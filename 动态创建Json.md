# C# dynamic 动态创建 json

根据键值对，动态生成Json

```c#
using Newtonsoft.Json;
using System;
using System.Collections.Generic;
using System.Dynamic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace AnuoDog.Csharp
{
    class StudyJsonNET
    {
        static void Main(string[] args)
        {
            dynamic objmatch = new ExpandoObject();

            Dictionary<string, string> matchKV = new Dictionary<string, string>();
            matchKV.Add("name", "jk");
            matchKV.Add("age","25");

            Dictionary<string, string> matchKV2 = new Dictionary<string, string>();
            matchKV2.Add("realName", "zs");
            matchKV2.Add("realAge", "9");

            List<dynamic> matchList = new List<dynamic>();
            matchList.Add(matchKV);
            matchList.Add(matchKV2);

            objmatch.match = matchList;

            dynamic obj = new ExpandoObject();
            obj.query = objmatch;
            obj.page = 5;

            string json = JsonConvert.SerializeObject(obj);
        }
    }
}
```

