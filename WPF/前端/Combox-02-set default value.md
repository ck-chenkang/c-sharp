```xaml
<StackPanel Orientation="Horizontal" Margin="0,10,0,0">
    <Label Content="串口:" VerticalAlignment="Center" Width="60"></Label>
    <ComboBox x:Name="serialPortCom" Width="100" ItemsSource="{Binding ViewModel.ComList}" SelectedIndex="0">
        <!--<ComboBoxItem Content="{Binding}" IsSelected="True" ></ComboBoxItem>-->
    </ComboBox>
</StackPanel>

<StackPanel Orientation="Horizontal" Margin="0,10,0,0">
    <Label Content="波特率:" VerticalAlignment="Center" Width="60"></Label>
    <ComboBox x:Name="baudRate" Width="100" ItemsSource="{Binding ViewModel.BaudRateList}" SelectedValue="9600">
    </ComboBox>
</StackPanel>
```

这两个关键属性：

SelectedIndex

SelectedValue