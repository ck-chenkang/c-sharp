# DataGrid通过数据绑定修改背景色

##  xaml

```xaml
<Window x:Class="WpfApp1.Window1"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfApp1"
        mc:Ignorable="d"
        Title="Name" Height="450" Width="800">


    <Grid>
        <DataGrid x:Name="myDataGrid" ItemsSource="{Binding}" AutoGenerateColumns="False">
            <DataGrid.Columns>
                <DataGridTextColumn Header="Name" Binding="{Binding Name}">
                    <DataGridTextColumn.CellStyle>
                        <Style TargetType="DataGridCell">
                            <Setter Property="Background" Value="{Binding Path=GridColor}" />
                            <!--<Setter Property="Background" Value="Green" />-->
                        </Style>
                    </DataGridTextColumn.CellStyle>
                </DataGridTextColumn>
            </DataGrid.Columns>
        </DataGrid>
    </Grid>

</Window>
```

## xaml.cs

```csharp
using System;
using System.Collections.Generic;
using System.Collections.ObjectModel;
using System.ComponentModel;
using System.Diagnostics.Metrics;
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
    public partial class Window1 : Window
    {
        public Window1()
        {
            InitializeComponent();
            Person person = new Person("名字", "Green");
            ObservableCollection<Person> persoonData = new ObservableCollection<Person>();
            persoonData.Add(person);
            this.myDataGrid.DataContext = persoonData;

        }

        public class Person : INotifyPropertyChanged
        {
            public event PropertyChangedEventHandler PropertyChanged;

            private string? _name;

            public string Name {
                get { return _name; }
                set {
                    _name = value;
                    if (this.PropertyChanged != null)
                    {
                        this.PropertyChanged.Invoke(this, new PropertyChangedEventArgs("Name"));
                        // 通知Binding是“Age”这个属性的值改变了
                    }
                }
            }

            private string _gridColor;
            public string GridColor { 
                get { return _gridColor; }
                set
                {
                    _gridColor = value;
                    if(this.PropertyChanged != null)
                    {
                        this.PropertyChanged.Invoke(this, new PropertyChangedEventArgs("GridColor"));
                    }
                }
            }

            public Person(string name, string gridColor)
            {
                Name = name;
                GridColor = gridColor;
            }
        }

    }
}
```

## 效果

![image-20221024092420473](E:\codes\c-sharp\WPF\前端\Imag\image-20221024092420473.png)