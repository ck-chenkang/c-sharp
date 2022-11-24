# ListView 布局属性 ItemsPanel

[官方文档](https://learn.microsoft.com/en-us/dotnet/api/system.windows.controls.itemscontrol.itemspanel?view=windowsdesktop-6.0)

这个是用来做ListView 的属性 ItemTemplate的布局的，要给他一个panel

```xaml
<ListView
          ItemsSource="{Binding ViewModel.StockDatasCollection, Mode=OneWay}"
          SelectedIndex="0" Grid.ColumnSpan="2">
    <ListView.ItemTemplate>
        <DataTemplate>
            <Border               
                    CornerRadius="4">
                <ui:Button    
                           Width="50"
                           Height="50"
                           Background="{Binding StatusColor}"
                           Content="{Binding No}"/>
            </Border>
        </DataTemplate>
    </ListView.ItemTemplate>
    <!--主要看这里-->
    <ListView.ItemsPanel>
        <ItemsPanelTemplate>
            <ui:VirtualizingWrapPanel
                                      Orientation="Vertical"
                                      SpacingMode="Uniform"
                                      StretchItems="False" />
        </ItemsPanelTemplate>
    </ListView.ItemsPanel>
</ListView>
```

