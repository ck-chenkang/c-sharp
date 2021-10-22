# Debug和Release判断

```csharp
class Program
{
    static void Main(string[] args)
    {
        #if DEBUG
            while (true)
            {
                Console.WriteLine("DEBUG");
                Thread.Sleep(6000);
            }
        #endif

            #if !DEBUG
            while (true)
            {
                Console.WriteLine("Release");
                Thread.Sleep(6000);
            }
        #endif
    }
}
```

