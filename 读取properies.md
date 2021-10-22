# c#读properties文件

## properties文件

```
MONGO_URL = mongodb://172.16.20.3/srtc_dc
CURRENT_VERSION = 2.0
IS_AUTO_UPDATE = no
REMOTE_UPDATE_FILE = http://192.168.1.121:8080/ClientBin.zip
REMOTE_VERSION_FILE = http://192.168.1.121:8080/version
PROGRAM_PATH = E:\dc\ClientBin\Wims.Mili.DC.Client.SYS.exe
```

## 源码

```
using System;
using System.Collections;
using System.IO;

namespace Wisdombud.Util
{
    public class PropertyOper : System.Collections.Hashtable
    {
        private string fileName = "";
        private ArrayList list = new ArrayList();
        public ArrayList List
        {
            get { return list; }
            set { list = value; }
        }
        /// <summary>
        /// 构造函数
        /// </summary>
        /// <param name="fileName">要读写的properties文件名</param>
        public PropertyOper(string fileName)
        {
            this.fileName = fileName;
            this.Load(fileName);
        }
        /// <summary>
        /// 重写父类的方法
        /// </summary>
        /// <param name="key">键</param>
        /// <param name="value">值</param>
        public override void Add(object key, object value)
        {
            base.Add(key, value);
            list.Add(key);

        }

        public void Update(object key, object value)
        {
            base.Remove(key);
            list.Remove(key);
            this.Add(key, value);

        }
        public override ICollection Keys
        {
            get
            {
                return list;
            }
        }
        /// <summary>
        /// 加载文件
        /// </summary>
        /// <param name="filePath">文件路径</param>
        private void Load(string filePath)
        {
            char[] convertBuf = new char[1024];
            int limit;
            int keyLen;
            int valueStart;
            char c;
            string bufLine = string.Empty;
            bool hasSep;
            bool precedingBackslash;
            using (StreamReader sr = new StreamReader(filePath))
            {
                while (sr.Peek() >= 0)
                {
                    bufLine = sr.ReadLine();
                    limit = bufLine.Length;
                    keyLen = 0;
                    valueStart = limit;
                    hasSep = false;
                    precedingBackslash = false;
                    if (bufLine.StartsWith("#"))
                        keyLen = bufLine.Length;
                    while (keyLen < limit)
                    {
                        c = bufLine[keyLen];
                        if ((c == '=' || c == ':') & !precedingBackslash)
                        {
                            valueStart = keyLen + 1;
                            hasSep = true;
                            break;
                        }
                        else if ((c == ' ' || c == '\t' || c == '\f') & !precedingBackslash)
                        {
                            valueStart = keyLen + 1;
                            break;
                        }
                        if (c == '\\')
                        {
                            precedingBackslash = !precedingBackslash;
                        }
                        else
                        {
                            precedingBackslash = false;
                        }
                        keyLen++;
                    }
                    while (valueStart < limit)
                    {
                        c = bufLine[valueStart];
                        if (c != ' ' && c != '\t' && c != '\f')
                        {
                            if (!hasSep && (c == '=' || c == ':'))
                            {
                                hasSep = true;
                            }
                            else
                            {
                                break;
                            }
                        }
                        valueStart++;
                    }
                    string key = bufLine.Substring(0, keyLen);
                    string values = bufLine.Substring(valueStart, limit - valueStart);
                    if (key == "")
                        key += "#";
                    while (key.StartsWith("#") & this.Contains(key))
                    {
                        key += "#";
                    }
                    this.Add(key, values);
                }
            }
        }
        /// <summary>
        /// 保存文件
        /// </summary>
        /// <param name="filePath">要保存的文件的路径</param>
        public void Save()
        {
            string filePath = this.fileName;
            if (File.Exists(filePath))
            {
                File.Delete(filePath);
            }
            FileStream fileStream = File.Create(filePath);
            StreamWriter sw = new StreamWriter(fileStream);
            foreach (object item in list)
            {
                String key = (String)item;
                String val = (String)this[key];
                if (key.StartsWith("#"))
                {
                    if (val == "")
                    {
                        sw.WriteLine(key);
                    }
                    else
                    {
                        sw.WriteLine(val);
                    }
                }
                else
                {
                    sw.WriteLine(key + "=" + val);
                }
            }
            sw.Close();
            fileStream.Close();
        }
    }
}
```

## 应用

```
        public static void ReadConfig()
        {
            PropertyOper po = new PropertyOper("update.properties");
            GlobalValues.MONGO_URL = po["MONGO_URL"].ToString();
            GlobalValues.IS_AUTO_UPDATE = po["IS_AUTO_UPDATE"].ToString().ToLower().Equals("yes") ? true : false;
            GlobalValues.REMOTE_UPDATE_FILE = po["REMOTE_UPDATE_FILE"].ToString();
            GlobalValues.REMOTE_VERSION_FILE = po["REMOTE_VERSION_FILE"].ToString();

            GlobalValues.PROGRAM_PATH = po["PROGRAM_PATH"].ToString();
            FileInfo fi = new FileInfo(GlobalValues.PROGRAM_PATH);
            GlobalValues.PROGRAM_FOLDER = fi.Directory.FullName;
            GlobalValues.PROGRAM_NAME = fi.Name.Replace(".exe", "");
            GlobalValues.CURRETN_VERSION = po["CURRENT_VERSION"].ToString();
            GetIP();
            DaoFactory.Init();
        }
```