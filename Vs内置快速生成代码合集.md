# VS 内置快捷键

输入简写，然后连敲两次tab键

| 首字母 | 简写             | 生成代码                                                     |
| ------ | ---------------- | ------------------------------------------------------------ |
| a      | attachedProperty | public static readonly ???  propertyNameProperty = ???.RegisterAttached(       "propertyName",       typeof(propertyType),       typeof(HomeController),       new  PropertyMetadata(default(propertyType)));          public static void SetpropertyName(DependencyObject element, propertyType  value)     {         element.SetValue(propertyNameProperty, value);     }          public static propertyType GetpropertyName(DependencyObject element)     {       return  (propertyType)element.GetValue(propertyNameProperty);     } |
|        | Attribute        | [AttributeUsage(AttributeTargets.All,  Inherited = false, AllowMultiple = true)]      private sealed class MyAttribute :  Attribute      {        // See the attribute guidelines  at         // http://go.microsoft.com/fwlink/?LinkId=85236        private readonly string  positionalString;             // This is a positional  argument        public MyAttribute(string  positionalString)        {          this.positionalString =  positionalString;               // TODO: Implement code  here          throw new  NotImplementedException();        }             public string PositionalString {  get; private set; }             // This is a named  argument        public int NamedInt { get; set;  }      } |
|        |                  |                                                              |
| c      | checked          |                                                              |
|        | class            |                                                              |
|        | ctor             | public A1()     {     }                                      |
|        | ctx              |                                                              |
|        | cw               | Console.WriteLine();                                         |
|        |                  |                                                              |
| d      | do               | do{          }while(ValidateRequest);                        |
|        |                  |                                                              |
| e      | ear              | TYPE[] types = new TYPE[] { };                               |
|        |                  |                                                              |
|        | enum             | enum MyEnum     {     }                                      |
|        | equals           |                                                              |
|        |                  |                                                              |
|        | Exception        |                                                              |
|        |                  |                                                              |
|        | else             |                                                              |
|        |                  |                                                              |
| f      | for              | for (int i = 0; i < UPPER;  i++)     {          }            |
|        |                  |                                                              |
|        | forr             | for (int i = length - 1; i >=  0; i--)     {          }      |
|        |                  |                                                              |
|        | foreach          | foreach (var VARIABLE in  COLLECTION)     {          }       |
|        |                  |                                                              |
|        | from             | from VAR in ViewEngineCollection       {          }          |
|        |                  |                                                              |
| h      | hal              | Html.ActionLink("TEXT", "ACTION",  "Account")                |
|        |                  |                                                              |
| i      |                  |                                                              |
|        | if               | if (ValidateRequest)     {     }                             |
|        |                  |                                                              |
|        | invoke           | EventHandler temp =  MyEvent;     if (temp != null)     {       temp();     } |
|        |                  |                                                              |
|        | ital             | for (int i = 0; i <  arrayList.Count; i++)     {        object array =  (object)arrayList[i];     } |
|        |                  |                                                              |
|        | itar             | for (int i = 0; i <  array.Length; i++)     {       var a = array[i];     } |
|        |                  |                                                              |
|        | itdg             | foreach (var i in  ViewData)     {       var key = i.Key;       var value = i.Value;     } |
|        |                  |                                                              |
|        | itdic            | foreach (DictionaryEntry  dictionaryEntry in dictionary)     {          object key =  (object)dictionaryEntry.Key;        object value =  (object)dictionaryEntry.Value;     } |
|        |                  |                                                              |
|        | itli             | for (int i = 0; i <  ViewEngineCollection.Count; i++)     {        object key =  (object)dictionaryEntry.Key;        object value =  (object)dictionaryEntry.Value;     } |
|        |                  |                                                              |
|        | indexer          | public object this[int index]      {           get           {              /* return the  specified index here */           }           set           {             /* set the specified  index to value here */           }     } |
|        |                  |                                                              |
|        | interface        | interface Iinterface     {     }                             |
|        |                  |                                                              |
|        | iterator         | public  System.Collections.Generic.IEnumerator<ElementType>  GetEnumerator()     {         throw new  NotImplementedException();         yield return default(ElementType);     } |
|        |                  |                                                              |
|        | iterindex        | public class MyViewIterator      {        private readonly MyViewIterator  outer;             internal  MyViewIterator(MyViewIterator outer)        {          this.outer = outer;        }             // TODO: provide an appropriate  implementation here        public int Length        {          get          {            return 1;          }        }             public ElementType this[int  index]        {          get          {            //            // TODO: implement  indexer here            //            // you have full access  to MyViewIterator privates            //            throw            new  NotImplementedException();            return  default(ElementType);          }        }             public  System.Collections.Generic.IEnumerator<ElementType>  GetEnumerator()        {          for (int i = 0; i <  this.Length; i++)          {            yield return  this[i];          }        }      } |
|        |                  |                                                              |
| l      | lock             | lock (ViewEngineCollection)     {          }                 |
|        |                  |                                                              |
| m      | mbox             | System.Windows.Forms.MessageBox.Show("Test");                |
|        |                  |                                                              |
| n      | nguid            | A509913F-295B-480F-A022-854A81045C6E                         |
|        |                  |                                                              |
| o      | out              | Console.Out.WriteLine("");                                   |
|        |                  |                                                              |
|        | outv             | Console.Out.WriteLine("ViewEngineCollection = {0}",  ViewEngineCollection); |
|        |                  |                                                              |
| p      | pci              | public const int                                             |
|        |                  |                                                              |
|        | pcs              | public const string                                          |
|        |                  |                                                              |
|        | prop             | public TYPE Type { get; set; }                               |
|        |                  |                                                              |
|        | propg            | public int I { get; private set; }                           |
|        |                  |                                                              |
|        | psr              | public static readonly                                       |
|        |                  |                                                              |
|        | psvm             | public static void Main(string[] args){}                     |
|        |                  |                                                              |
| r      | rta              | RedirectToAction("ACTION", "Account")                        |
|        |                  |                                                              |
|        | ritar            | for (int i = array.Length - 1; i  >= 0; i--)     {        var a = array[i];     } |
|        |                  |                                                              |
| s      | sfc              | var type = ViewEngineCollection  as TYPE;          if (type != null)     {            } |
|        |                  |                                                              |
|        | switch           | switch (@enum)     {              }                          |
|        |                  |                                                              |
|        | svm              | static void Main(string[]  args)     {             }         |
|        |                  |                                                              |
|        | sim              | static int Main(string[]  args)     {                return 0;     } |
|        |                  |                                                              |
|        | struct           | struct MyStruct     {             }                          |
|        |                  |                                                              |
| t      | thr              | throw new                                                    |
|        |                  |                                                              |
|        | toar             | (object[])arrayList.ToArray(typeof(object))                  |
|        |                  |                                                              |
|        | try              | try     {          }     catch (Exception)     {              throw;     } |
|        |                  |                                                              |
|        | tryf             | try     {          }     finally     {            }          |
|        |                  |                                                              |
| u      | ua               | Url.Action("ACTION", "Account")                              |
|        |                  |                                                              |
|        | unchecked        | unchecked     {            }                                 |
|        |                  |                                                              |
|        | unsafe           | unsafe     {            }                                    |
|        |                  |                                                              |
|        | using            | using (this)     {             }                             |
|        |                  |                                                              |
| w      | while            | while (true)     {             }                             |

