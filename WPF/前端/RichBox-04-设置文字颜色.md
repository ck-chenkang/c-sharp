[WPF RichTextBox appending coloured text](https://stackoverflow.com/questions/5512921/wpf-richtextbox-appending-coloured-text)

```c#
// 给richbox 添加行内文本 + 设置颜色
private void AppendText(RichTextBox box, string text, string color)
{
    BrushConverter bc = new BrushConverter();
    TextRange tr = new TextRange(box.Document.ContentEnd, box.Document.ContentEnd);
    tr.Text = text;
    try
    {
        // 设置颜色
        tr.ApplyPropertyValue(TextElement.ForegroundProperty,
                              bc.ConvertFromString(color));
        // 设置字体大小
        tr.ApplyPropertyValue(TextElement.FontSizeProperty,
                              "50");
    }
    catch (FormatException) { }
}
```

