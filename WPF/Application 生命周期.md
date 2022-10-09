# 生命周期 

我们知道webform中的Global文件定义了一个应用程序的全局生命周期，或许有人问，生命周期能够干些什么，其实干的事情可多着呢，

比如我们可以做一些身份验证，或者一些信息的初始化，那么wpf中到底有哪些对应的方法和事件呢？

1：OnStartup方法   =>  Startup 事件

   这个就见名识意了，也就是上面一幅图中的app.Run()的时候触发。

2: OnSessionEnding方法 => SessionEnding 事件

   系统关机前调用。

3：OnExit方法 => Exit事件

   应用程序关闭前调用。

4：OnActivated方法 =>  Activated 事件

   应用程序获得焦点的时候触发。

5：OnDeactivated方法 => DeActivated事件

   应用程序失去焦点的时候触发。

```csharp
using System;
using System.Collections.Generic;
using System.Configuration;
using System.Data;
using System.Linq;
using System.Threading.Tasks;
using System.Windows;

namespace Test
{
    /// <summary>
    /// App.xaml 的交互逻辑
    /// </summary>
    public partial class App : Application
    {
        protected override void OnActivated(EventArgs e)
        {
            base.OnActivated(e);
            //TODO  your code
        }

        protected override void OnDeactivated(EventArgs e)
        {
            base.OnDeactivated(e);
           //TODO  your code
        }

        protected override void OnExit(ExitEventArgs e)
        {
            base.OnExit(e);
            //TODO  your code
        }

        protected override void OnStartup(StartupEventArgs e)
        {
            base.OnStartup(e);
            //TODO  your code

        }

        protected override void OnSessionEnding(SessionEndingCancelEventArgs e)
        {
            base.OnSessionEnding(e);
            //TODO  your code

        }
    }
}
```