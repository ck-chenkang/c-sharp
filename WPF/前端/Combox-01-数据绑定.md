```xaml
<StackPanel Orientation="Horizontal" Margin="0,10,0,0">
    <Label Content="波特率:" VerticalAlignment="Center" Width="60"></Label>
    <ComboBox x:Name="baudRate" Width="100" ItemsSource="{Binding ViewModel.BaudRateList}" SelectedValue="9600">
    </ComboBox>
</StackPanel>
```

