​                                            

[项目源码](https://download.csdn.net/download/qq_43511299/49074909)

## **GroupBox控件** 

GroupBox的标题属性：[Header](https://so.csdn.net/so/search?q=Header&spm=1001.2101.3001.7020)=“GroupBox”
 在GroupBox中可以放置其他布局容器，例如StackPannel。

![在这里插入图片描述](E:\codes\c-sharp\WPF\控件\Imag\46c679361dc84accb80ad815a07fbe59.png)

```xml
<GroupBox x:Name="groupBox" Header="GroupBox">
    <StackPanel>
        <RadioButton Content="1" Margin="10"/>
        <RadioButton Content="2" Margin="10"/>
        <RadioButton Content="3" Margin="10"/>
        <Button Height="50" Width=" 300" Margin="30" Content="Save"/>
    </StackPanel>
</GroupBox>
12345678
```

## **TabControl控件** 

Tab位置的属性`TabStripPlacement="Bottom"`默认情况下设置为Top，可以设在四周其他位置Left, Right。
 TabControl控件中包含TabItem，TabItem中又可以包含像StackPannel这样的容器。

```xml
<TabControl x:Name="tabControl" TabStripPlacement="Top">
    <TabItem Name="Tab1">
        <TabItem.Header>
            <StackPanel>
                <TextBlock Margin="3">
                    Image and text
                </TextBlock>
                <Image Source="/d6302eeec39695060de3ec3ab5404024.jpg" Width="20" Height="20"> 
                </Image>
            </StackPanel>
        </TabItem.Header><!--用元素属性定义标题，使标题内也可以包含容器-->
        <StackPanel Name="stackPannel1" Margin="3">
            <CheckBox Content="Setting1" Margin="3"/>
            <CheckBox Content="Setting2" Margin="3"/>
            <CheckBox Content="Setting3" Margin="3"/>
        </StackPanel>
    </TabItem>
    <TabItem Header="TabItem" Name="Tab2">
        <StackPanel Name="stackPannel2" Margin="3"/>
    </TabItem>
    <TabItem Header="TabItem" Name="Tab3">
        <StackPanel Name="stackPannel3" Margin="3"/>
    </TabItem>
</TabControl>
123456789101112131415161718192021222324
```

![在这里插入图片描述](E:\codes\c-sharp\WPF\控件\Imag\730ce2863a4843a29630f091bb6190d2.png)
 可以通过代码来选择TabItem.
 防止按钮并定义点击事件响应函数：

```csharp
private void Button_Click(object sender, RoutedEventArgs e)
{
    this.Tab2.IsSelected = true;
}
1234
```

## **Expander控件** 

Expander控件可以放置大量内容，并且通过折叠清晰呈现数据。
 如果窗体不够大，内容无法完全显示，可以设置窗体属性：`SizeToContent="Height"`使得窗体高度随着内容大小改变。
 在Expander控件中放置ScrollViewer控件，在ScrollViewer控件中防止TextBlock控件，还可以修改Expander的折叠方向`ExpandDirection="Right"`使内容向右展开。

```xml
<StackPanel Margin="3">
    <Expander Header="Expander1" Margin="5" Padding="5">
        <Button Width=" 100" Height="50"/>
    </Expander>
    <Expander Header="Expander2" Margin="5" Padding="5" ExpandDirection="Right">
        <ScrollViewer VerticalScrollBarVisibility="Visible" Height="100">
            <TextBlock Text="视频提供了功能强大的方法帮助您证明您的观点。当您单击联机视频时，可以在想要添加的视频的嵌入代码中进行粘贴。您也可以键入一个关键字以联机搜索最适合您的文档的视频。为使您的文档具有专业外观，Word 提供了页眉、页脚、封面和文本框设计，这些设计可互为补充。例如，您可以添加匹配的封面、页眉和提要栏。单击，然后从不同库中选择所需元素。主题和样式也有助于文档保持协调。当您单击设计并选择新的主题时，图片、图表或 SmartArt 图形将会更改以匹配新的主题。当应用样式时，您的标题会进行更改以匹配新的主题。使用在需要位置出现的新按钮在 Word 中保存时间。
若要更改图片适应文档的方式，请单击该图片，图片旁边将会显示布局选项按钮。当处理表格时，单击要添加行或列的位置，然后单击加号。在新的阅读视图中阅读更加容易。可以折叠文档某些部分并关注所需文本。如果在达到结尾处之前需要停止读取，Word 会记住您的停止位置 - 即使在另一个设备上。视频提供了功能强大的方法帮助您证明您的观点。当您单击联机视频时，可以在想要添加的视频的嵌入代码中进行粘贴。您也可以键入一个关键字以联机搜索最适合您的文档的视频。为使您的文档具有专业外观，Word 提供了页眉、页脚、封面和文本框设计，这些设计可互为补充。例如，您可以添加匹配的封面、页眉和提要栏。" TextWrapping="Wrap"/>
        </ScrollViewer>
    </Expander>
    <Expander Header="Expander3"  Margin="5" Padding="5">
        <Button Width="100" Height="50"/>
    </Expander>
</StackPanel>
1234567891011121314
```

![在这里插入图片描述](E:\codes\c-sharp\WPF\控件\Imag\a2dd7c961bea44f4a1d7768d4a56f485.png)