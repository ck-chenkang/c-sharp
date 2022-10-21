# ListView

## DataBinding没有ItemTemplate

```xaml
<Window x:Class="WpfTutorialSamples.ListView_control.ListViewDataBindingSample"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="ListViewDataBindingSample" Height="300" Width="300">
    <Grid>
		<ListView Margin="10" Name="lvDataBinding"></ListView>
	</Grid>
</Window>
```

```csharp
using System;
using System.Collections.Generic;
using System.Windows;

namespace WpfTutorialSamples.ListView_control
{
	public partial class ListViewDataBindingSample : Window
	{
		public ListViewDataBindingSample()
		{
			InitializeComponent();
			List<User> items = new List<User>();
			items.Add(new User() { Name = "John Doe", Age = 42 });
			items.Add(new User() { Name = "Jane Doe", Age = 39 });
			items.Add(new User() { Name = "Sammy Doe", Age = 13 });
			lvDataBinding.ItemsSource = items;
		}
	}

	public class User
	{
		public string Name { get; set; }

		public int Age { get; set; }
	}
}
```

![image-20221021153628025](E:\codes\c-sharp\WPF\前端\Imag\image-20221021153628025.png)

```csharp
public class User
{
	public string Name { get; set; }

	public int Age { get; set; }

	public override string ToString()
	{
		return this.Name + ", " + this.Age + " years old";
	}
}
```

![image-20221021153653830](E:\codes\c-sharp\WPF\前端\Imag\image-20221021153653830.png)



## 有ItemTemplate

```xaml
<Window x:Class="WpfTutorialSamples.ListView_control.ListViewItemTemplateSample"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="ListViewItemTemplateSample" Height="150" Width="350">
    <Grid>
		<ListView Margin="10" Name="lvDataBinding">
			<ListView.ItemTemplate>
				<DataTemplate>
					<WrapPanel>
						<TextBlock Text="Name: " />
						<TextBlock Text="{Binding Name}" FontWeight="Bold" />
						<TextBlock Text=", " />
						<TextBlock Text="Age: " />
						<TextBlock Text="{Binding Age}" FontWeight="Bold" />
						<TextBlock Text=" (" />
						<TextBlock Text="{Binding Mail}" TextDecorations="Underline" Foreground="Blue" Cursor="Hand" />
						<TextBlock Text=")" />
					</WrapPanel>
				</DataTemplate>
			</ListView.ItemTemplate>
		</ListView>
	</Grid>
</Window>
```

```cs
using System;
using System.Collections.Generic;
using System.Windows;

namespace WpfTutorialSamples.ListView_control
{
	public partial class ListViewItemTemplateSample : Window
	{
		public ListViewItemTemplateSample()
		{
			InitializeComponent();
			List<User> items = new List<User>();
			items.Add(new User() { Name = "John Doe", Age = 42, Mail = "john@doe-family.com" });
			items.Add(new User() { Name = "Jane Doe", Age = 39, Mail = "jane@doe-family.com" });
			items.Add(new User() { Name = "Sammy Doe", Age = 13, Mail = "sammy.doe@gmail.com" });
			lvDataBinding.ItemsSource = items;
		}
	}

	public class User
	{
		public string Name { get; set; }

		public int Age { get; set; }

		public string Mail { get; set; }
	}
}
```

![image-20221021153808005](E:\codes\c-sharp\WPF\前端\Imag\image-20221021153808005.png)