## xmal:

```xaml
<Window x:Class="WpfApp1.Window1"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfApp1"
        mc:Ignorable="d"
        Title="Name" Height="450" Width="800">

    <Window.Resources>
        <DataTemplate x:Key="myDataTemplate">
            <Grid>
                <Label Content="{Binding  Path=Age}" FontSize="50"></Label>
            </Grid>
        </DataTemplate>
    </Window.Resources>

    <Grid>   
        <ContentControl x:Name="myContentControl" Content="{Binding}"  ContentTemplate="{StaticResource myDataTemplate}"></ContentControl>
    </Grid>    
</Window>
```

## xaml.cs:

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
using System.Windows.Interop;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Shapes;

namespace WpfApp1
{
    /// <summary>
    /// Window1.xaml 的交互逻辑
    /// </summary>
    public partial class Window1 : Window
    {
        Person myPerson;
        public Window1()
        {
            InitializeComponent();
            myPerson = new Person();
            myPerson.Age = 11;
            this.myContentControl.DataContext = myPerson;

        }
        private bool _isDataDirty;   

        private void documentTextBox_TextChanged(object sender, TextChangedEventArgs e) =>
            _isDataDirty = true;

        private void Window_Closing(object sender, System.ComponentModel.CancelEventArgs e)
        {
            // If data is dirty, prompt user and ask for a response
            if (_isDataDirty)
            {
                var result = MessageBox.Show("Document has changed. Close without saving?",
                                             "Question",
                                             MessageBoxButton.YesNo);

                // User doesn't want to close, cancel closure
                if (result == MessageBoxResult.No)
                    e.Cancel = true;
            }
        }
    }

    public class Person: INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged; 

        private int age;
        public int Age
        {
            get { return age; }
            set
            {
                age = value;
                if (this.PropertyChanged != null)
                {
                    this.PropertyChanged.Invoke(this, new PropertyChangedEventArgs("Age"));
                    // 通知Binding是“Age”这个属性的值改变了
                }
            }
        }
    }
}
```

## 效果：

![image-20221021141025214](E:\codes\c-sharp\WPF\前端\Imag\image-20221021141025214.png)

