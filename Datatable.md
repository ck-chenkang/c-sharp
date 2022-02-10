# Datatable

## 遍历Datatable的方法

```c# 
// 方法一：     
DataTable dt = dataSet.Tables[0];     
for(int i = 0 ; i < dt.Rows.Count ; i++)     
{     
   string strName = dt.Rows[i]["字段名"].ToString();     
}     
      
// 方法二：     
foreach(DataRow myRow in myDataSet.Tables["temp"].Rows)     
{     
      var str = myRow[0].ToString();     
}     
      
// 方法三：     
foeach(DataRow dr in dt.Rows)        
{        
     object value = dr["ColumnsName"];        
}     
      
// 方法四：     
DataTable dt=new DataTable();        
foreach(DataRow dr in dt.Rows)        
{      
   for(int i=0;i<dt.Columns.Count;i++)      
   {      
dr[i];      
   }        
}     
      
// 绑定DataTable到Reapter。     
if (dtb_xx.Rows.Count > 0)     
        {     
            rp_xx.DataSource = dtb_xx;     
            rp_xx.DataBind();     
        }      
<asp:Repeater ID="rp_xx" runat="server">     
       <ItemTemplate>     
            <tr>     
                  <td>     
                      <div>     
                            <ul class="ListHorizontally">     
                                 <li>     
                                      <div class="TCell1">     
                                            <%#Eval("ID")%>     
                                       </div>     
                                  </li>     
                                  <li>     
                                       <div class="TCell2">     
                                             <%#Eval("Name")%>     
                                        </div>     
                                  </li>     
                            </ul>     
                       </div>     
                    </td>     
                </tr>     
            </ItemTemplate>     
         </asp:Repeater>     
// 方法五  
DataRow[] dataRows = null;  
dataRows = dataTable.Select(fieldParentID + "='" + treeNode.Tag.ToString() + "'", dataTable.DefaultView.Sort);  
foreach (DataRow dataRow in dataRows)  
{   
    
     DataRow dataRow = dataTable.Rows[i];   
    
     ?? = dataRow[fieldParentID].ToString();  
}   
```

