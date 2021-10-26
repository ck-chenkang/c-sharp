## 封装类

```csharp
using DaPingBackEnd.Log;
using MySql.Data.MySqlClient;
using System;
using System.Collections.Generic;
using System.Data;
using System.Linq;
using System.Text;
using System.Threading.Tasks;


namespace DaPingBackEnd.MysqlServerBase
{
    class MysqlCtl
    {
        

        public MySqlConnection con
        {
            get;
            private set;
        }

        public readonly MySqlDataAdapter sda = new MySqlDataAdapter();

        private DataSet Ds = new DataSet();

        public DataSet ds
        {
            get { return Ds; }
        }

        private DataTable Dt = new DataTable();

        public DataTable dt
        {
            get { return Dt; }
        }


        public int connectToSQL(string connStr)
        {
            try
            {
                con = new MySqlConnection(connStr);
            }
            catch (Exception e)
            {
                Logctl.ShowError(e);
                return -1;
            }
            return 0;
        }

        // 增删改
        public int handleSql(string com)
        {
            if (null == con)
            {
                Logctl.ShowError(new Exception("未初始化数据库连接"));
                return -2;
            }

            try
            {
                MySqlCommand commad = new MySqlCommand(com, con);
                con.Open();
                commad.ExecuteNonQuery();
                con.Close();
            }
            catch (Exception e)
            {
                Logctl.ShowError(e);
                if (con.State == ConnectionState.Open)
                {
                    con.Close();
                }
                return -1;
            }
            return 0;
        }

        public int checkToDataSet(string sql)
        {
            if (null == con)
            {
                Logctl.ShowError(new Exception("未初始化数据库连接"));
                return -2;
            }
            try
            {
                MySqlCommand MyCommand = new MySqlCommand(sql, con); //定义一个数据库操作指令
                sda.SelectCommand = MyCommand;//设置操作指令
                con.Open();//打开数据库连接
                sda.SelectCommand.ExecuteNonQuery();//执行数据库查询指令
                Ds = new DataSet();
                sda.Fill(Ds);
                con.Close();//关闭数据库连接
            }
            catch (Exception e)
            {
                if (con.State == ConnectionState.Open)
                {
                    con.Close();
                }
                Logctl.ShowError(e);
                return -1;
            }
            return 0;
        }


        public int checkToDataTable(string sql)
        {
            int re = checkToDataSet(sql);
            if (0 == re)
                Dt = Ds.Tables[0];
            return re;
        }
    }
}
```

## 调用方法，查看同目录下Sql server封装