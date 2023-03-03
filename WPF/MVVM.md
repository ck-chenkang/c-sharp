# MVVM

## **一.MVVM模式简介** 

### 1.MVVM

MVVM是Model、View、ViewModel的简写，这种模式的引入就是使用ViewModel来降低View和Model的耦合，说是降低View和Model的耦合。也可以说是降低界面和逻辑的耦合，理想情况下界面和逻辑是完全分离的，单方面更改界面时不需要对逻辑代码改动，同样的逻辑代码更改时也不需要更改界面。同一个ViewModel可以使用完全不同的View进行展示，同一个View也可以使用不同的ViewModel以提供不同的操作。

 ![img](E:\codes\c-sharp\WPF\Imag\20161125103948984)




### 2.Model

 Model就是一个class，是对现实中事物的抽象，开发过程中涉及到的事物都可以抽象为Model，例如客户，客户的姓名、编号、电话、住址等属性也对应了class中的Property，客户的下订单、付款等行为对应了class中的方法。

### 3. View

 View很好理解，就是界面。对应WPF中的xaml界面设计。

### 4. ViewModel

 上面说过Model抽象，那么ViewModel就是对View的抽象。显示的数据对应着ViewMode中的Property，执行的命令对应着ViewModel中的Command。

###  5.WPF中MVVM的解耦方式

  在WPF的MVVM模式中，View和ViewModel之间数据和命令的关联都是通过绑定实现的，绑定后View和ViewModel并不产生直接的依赖。具体就是View中出现数据变化时会尝试修改绑定的目标。同样View执行命令时也会去寻找绑定的Command并执行。反过来，ViewModel在Property发生改变时会发个通知说“名字叫XXX的Property改变了，你们这些View中谁绑定了XXX也要跟着变啊!”，至于有没有View收到是不是做出变化也不关心。ViewModel中的Command脱离View就更简单了，因为Command在执行操作过程中操作数据时，根本不需要操作View中的数据，只需要操作ViewModel中的Property就可以了，Property的变化通过绑定就可以反映到View上。这样在测试Command时也不需要View的参与。这也是我在接触WPF初期时根本理解不了的所谓数据驱动。
 这样一来ViewMode可以在完全没有View的情况下测试，View也可以在完全没有ViewModel的情况下测试(当然只是测试界面布局和动画等业务无关的内容)。



  

## 二.数据绑定 

首先定义NotificationObject类。目的是绑定数据属性。这个类的作用是实现了INotifyPropertyChanged接口。WPF中类要实现这个接口，其属性成员才具备通知UI的能力在Prism中有一个NotificationObject自动实现了这个接口，位于Microsoft.Practices.Prism.ViewModel命名空间下。也就是说，Prism推荐ViewModel继承这个NotificationObject类来自动实现INotifyPropertyChanged接口。

### 1.定义Model



```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Practices.Prism.Commands;
using Microsoft.Practices.Prism.ViewModel;
namespace WpfMsgReport.Model
{
    //航次号Model
    class BaseCommonModel:NotificationObject
    {
        private string code;
        public string Code
        {
            get { return code; }
            set
            {
                code = value;
                this.RaisePropertyChanged("Code");
            }
        }
        private string name;
        public string Name
        {
            get { return name; }
            set
            {
                name = value;
                this.RaisePropertyChanged("Name");
            }
        }
        private string other;
        public string Other
        {
            get { return other; }
            set
            {
                other = value;
                this.RaisePropertyChanged("Other");
            }
        }
    }
}
```

### 2.定义ViewModel：ViewModel有属性VoyNoList





```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Practices.Prism.Commands;
using Microsoft.Practices.Prism.ViewModel;
using System.Windows.Forms;
using WpfMsgReport.Model;
namespace WpfMsgReport.ViewModel
{
    //主页面ViewModel
    class MainWindowViewModel : NotificationObject
    {
        /// <summary>
        /// 航次号列表
        /// </summary>
        private List<BaseCommonModel> voyNoList;
        public List<BaseCommonModel> VoyNoList
        {
            get { return voyNoList; }
            set
            {
                voyNoList = value;
                this.RaisePropertyChanged("VoyNoList");
            }
        }
        public MainWindowViewModel(HelpNavigator MyNavigator)
        {
            //载入主界面数据
            this.loadMainData();
        }
        /// <summary>
        /// 载入主界面数据
        /// </summary>
        private void loadMainData()
        {
            //载入航次号列表
            this.VoyNoList = new List<BaseCommonModel>();
            BaseCommonModel voyNoModel = new BaseCommonModel();
            voyNoModel.Code = "10000";
            voyNoModel.Name = "10000";
            VoyNoList.Add(voyNoModel);
            BaseCommonModel voyNoModel1 = new BaseCommonModel();
            voyNoModel1.Code = "10001";
            voyNoModel1.Name = "10001";
            VoyNoList.Add(voyNoModel1);
        }
    }
}
```

### 3.View控件绑定ViewModel的属性VoyNoList

```html
<ComboBox x:Name="voyNoList" ItemsSource="{Binding VoyNoList}" DisplayMemberPath="Name" SelectedValuePath="Code" SelectionChanged="voyNoList_SelectionChanged"/>
```



xaml对应的.cs的DataContext设置为MainWindowViewModel

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using WpfMsgReport.Model;
using WpfMsgReport.ViewModel;
namespace WpfMsgReport
{
    /// <summary>
    /// MainWindow.xaml 的交互逻辑
    /// </summary>
    public partial class MainWindow : Window
    {
        System.Windows.Forms.HelpNavigator MyNavigator = System.Windows.Forms.HelpNavigator.TableOfContents;
        public MainWindow()
        {
            InitializeComponent();
            this.DataContext = new MainWindowViewModel(MyNavigator);
        }
    }
}
```

实现效果：  

![img](E:\codes\c-sharp\WPF\Imag\20161125113530869)



 

## 三.命令绑定 

### 1.ViewModel定义命令并绑定实现方法

  ![img](E:\codes\c-sharp\WPF\Imag\20161125133718498)


  ![img](E:\codes\c-sharp\WPF\Imag\20161125133727373)


  ![img](E:\codes\c-sharp\WPF\Imag\20161125133739424)


  代码如下： 



```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Practices.Prism.Commands;
using Microsoft.Practices.Prism.ViewModel;
using System.Windows.Forms;
using WpfMsgReport.Model;
using System.Windows;
namespace WpfMsgReport.ViewModel
{
    //主页面ViewModel
    class MainWindowViewModel : NotificationObject
    {
        /// <summary>
        /// 航次号列表
        /// </summary>
        private List<BaseCommonModel> voyNoList;
        public List<BaseCommonModel> VoyNoList
        {
            get { return voyNoList; }
            set
            {
                voyNoList = value;
                this.RaisePropertyChanged("VoyNoList");
            }
        }
        ///命令
        public DelegateCommand<object> SendMailCommand { get; set; }    //发送报文按钮
        public MainWindowViewModel(HelpNavigator MyNavigator)
        {
            this.SendMailCommand = new DelegateCommand<object>(SendMailCommandExecute);
            //载入主界面数据
            this.loadMainData();
        }
        /// <summary>
        /// 载入主界面数据
        /// </summary>
        private void loadMainData()
        {
            //载入航次号列表
            this.VoyNoList = new List<BaseCommonModel>();
            BaseCommonModel voyNoModel = new BaseCommonModel();
            voyNoModel.Code = "10000";
            voyNoModel.Name = "10000";
            VoyNoList.Add(voyNoModel);
            BaseCommonModel voyNoModel1 = new BaseCommonModel();
            voyNoModel1.Code = "10001";
            voyNoModel1.Name = "10001";
            VoyNoList.Add(voyNoModel1);
        }
        /// <summary>
        /// 选择报文，发送邮件
        /// </summary>
        /// <param name="obj"></param>
        private void SendMailCommandExecute(object obj)
        {
            UIElement ui = obj as UIElement;
            if (ui != null)
            {
                if (ui.GetType().Name == "DataGrid")
                {
                    System.Windows.Controls.DataGrid dg = ui as System.Windows.Controls.DataGrid;
                    var a = dg.SelectedItem;
                    System.Windows.Forms.MessageBox.Show("发送邮件");
                }
            }
        }
    }
}
```

### 2.在xaml的控件绑定命令，并把界面控件作参数传递到ViewModel的方法中

  ![img](E:\codes\c-sharp\WPF\Imag\20161125133805393)


  代码如下： 



```html
<Button Width="100" Cursor="Hand" Background="White" BorderBrush="White" Command="{Binding Path=SendMailCommand}" CommandParameter="{Binding ElementName=reportListDataGrid}">
    <StackPanel Orientation="Horizontal">
        <Image HorizontalAlignment="Center" VerticalAlignment="Center" Source="/WpfMsgReport;component/Images/email.gif" Height="16"/>
        <TextBlock Text="发送邮件" Width="70" HorizontalAlignment="Center" VerticalAlignment="Center" Margin="2,0,0,0" />
    </StackPanel>
</Button>
```

### 3.实现效果

  ![img](E:\codes\c-sharp\WPF\Imag\20161125132808075)
        

## 四.事件绑定 

 [WPF](https://so.csdn.net/so/search?q=WPF&spm=1001.2101.3001.7020)中不是所有的控件都有Command属性的，如窗体，如果需要在ViewModel中处理Loaded事件命令，或者其他事件的命令时，很难通过绑定Command完成，必须要注册依赖属性或事件等，太麻烦了。我喜欢简约、有效的方式，现在我和大家一起分享一下。

 场景，我需要处理ComboBox的SelectionChanged事件，但又避免用后置代码，尽量要在ViewModel中获取。这是需要一个System.Windows.Interactivity.dll，该dll是安装Blend后才有的，在C:\Program Files\Microsoft SDKs\Expression\Blend\.NETFramework\v4.0\Libraries目录中，然后我们仍需要Prism.dll。

###  1.在ViewModel定义命令ChangeVoyNoCommand

  ![img](E:\codes\c-sharp\WPF\Imag\20161125141008436)  



 

### 2.在ViewModel实现方法ChangeVoyNoCommandExecute

  ![img](E:\codes\c-sharp\WPF\Imag\20161125141105531)  


### 3.在xaml中导入System.Windows.Interactivity.dll

  ![img](E:\codes\c-sharp\WPF\Imag\20161125141225656)


### 4.在控件ComboBox上绑定事件SelectionChanged和命令ChangeVoyNoCommand

   

```html
<ComboBox x:Name="voyNoList" ItemsSource="{Binding VoyNoList,UpdateSourceTrigger=PropertyChanged}" SelectedValue="{Binding Path=SelectVoyNo, UpdateSourceTrigger=PropertyChanged}" DisplayMemberPath="Name" SelectedValuePath="Code">
	<i:Interaction.Triggers>
		<i:EventTrigger EventName="SelectionChanged">
			<i:InvokeCommandAction Command="{Binding ChangeVoyNoCommand}"/>
		</i:EventTrigger>
	</i:Interaction.Triggers>
</ComboBox>
```

### 5.实现效果

  ![img](E:\codes\c-sharp\WPF\Imag\20161125141558829)



 or
