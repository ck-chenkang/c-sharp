## Class

```csharp
class Log
{
    //用来判断当前log.txt的大小，如果大于2M，就会把它重命名，然后移个位置
    public static void dealLogFiles()
    {
        string fullFilePath = "log//log.txt";
        string dirPath = Path.GetDirectoryName(fullFilePath);
        string fileName = Path.GetFileNameWithoutExtension(fullFilePath);
        if (!Directory.Exists(dirPath))
        {
            Directory.CreateDirectory(dirPath);
        }
        if (!File.Exists(fullFilePath))
        {
            using (File.Create(fullFilePath)) { }
        }

        FileInfo fileinfo = new FileInfo(fullFilePath);
        if (fileinfo.Length > 2 * 1024 * 1024)
        {
            File.Move(fullFilePath, dirPath + "//" + DateTime.Now.ToFileTime().ToString() + ".txt");

            if (!File.Exists(fullFilePath))
            {
                using (File.Create(fullFilePath)) { }
            }
        }
    }
}
```

## 用法

```csharp
try{

}
catch (Exception e)
{
    Console.WriteLine(DateTime.Now.ToString() + "\r\n" + e.Message + "\r\n" + e.StackTrace + "\r\n\r\n");
    Log.dealLogFiles();
    File.AppendAllText("log//log.txt", DateTime.Now.ToString() + "\r\n" + e.Message + "\r\n" + e.StackTrace + "\r\n\r\n");
}
```

