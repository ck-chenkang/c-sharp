# Main函数

我们新建一个wpf的程序，vs自动给我们生成了一个MainWindow.xaml和App.xaml文件。

微软官方说wpf程序是从Application开始的，既然是开始总有个入口点吧，奇怪的是我们并没有发现Main函数，程序又是如何Run起来的呢？

其实，wpf为了简化我们的工作，把一些机械性的代码透明了，那么我们如何找到这个Main函数呢？很简单，我们编译一下程序，发现

App.[xaml](https://so.csdn.net/so/search?q=xaml&spm=1001.2101.3001.7020)最后生成了App.g.cs的部分类，并且发现StartupUri是MainWindow.xaml，也就是说程序一运行，MainWindow.xaml将会启动。

![img](E:\codes\c-sharp\WPF\Imag\20161123140045247)