---
title: "使用 DataReader 检索数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97afc121-fb8b-465b-bab3-6d844420badb
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 使用 DataReader 检索数据
使用 **DataReader** 检索数据包括创建 **Command** 对象的实例，然后通过调用 **Command.ExecuteReader** 创建一个 **DataReader**，以便从数据源检索行。  下面的示例演示如何使用 **DataReader**，其中 `reader` 表示有效的 DataReader，而 `command` 表示有效的 Command 对象。  
  
```  
reader = command.ExecuteReader();  
```  
  
 使用 **DataReader** 对象的 **Read** 方法可从查询结果中获取行。  通过向 **DataReader** 传递列的名称或序号引用，可以访问返回行的每一列。  不过，为了实现最佳性能，**DataReader** 提供了一系列方法，将使您能够访问其本机数据类型（**GetDateTime**、**GetDouble**、**GetGuid**、**GetInt32** 等）的列值。  有关数据提供程序特定的 **DataReaders** 的类型化访问器方法列表，请参见 <xref:System.Data.OleDb.OleDbDataReader> 和 <xref:System.Data.SqlClient.SqlDataReader>。  假定基础数据类型为已知，如果使用类型化访问器方法，将减少在检索列值时所需的类型转换量。  
  
> [!NOTE]
>  .NET Framework 的 Windows Server 2003 版包含 **DataReader** 的附加属性 **HasRows**，该属性使您能够在读取 **DataReader** 之前就可确定它是否返回了任何结果。  
  
 以下代码示例循环访问一个 **DataReader** 对象，并从每个行中返回两个列。  
  
 [!code-csharp[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/VB/source.vb#1)]  
  
 **DataReader** 提供未缓冲的数据流，该数据流使过程逻辑可以有效地按顺序处理从数据源中返回的结果。  由于数据不在内存中缓存，所以在检索大量数据时，**DataReader** 是一种适合的选择。  
  
## 关闭 DataReader  
 每次使用完 **DataReader** 对象后都应调用 **Close** 方法。  
  
 如果 **Command** 包含输出参数或返回值，那么在 **DataReader** 关闭之前，将无法访问这些输出参数或返回值。  
  
 请注意，当 **DataReader** 打开时，该 **DataReader** 将以独占方式使用 **Connection**。  在原始 **DataReader** 关闭之前，将无法对 **Connection** 执行任何命令（包括创建另一个 **DataReader**）。  
  
> [!NOTE]
>  不要在类的 **Finalize** 方法中对 **Connection**、**DataReader** 或任何其他托管对象调用 **Close** 或 **Dispose**。  在终结器中，仅释放类直接拥有的非托管资源。  如果类不拥有任何非托管资源，则不要在类定义中包含 **Finalize** 方法。  有关详细信息，请参阅[Garbage Collection](../../../../docs/standard/garbage-collection/index.md)。  
  
## 使用 NextResult 检索多个结果集  
 如果返回的是多个结果集，**DataReader** 会提供 **NextResult** 方法来按顺序循环访问这些结果集。  以下示例显示 <xref:System.Data.SqlClient.SqlDataReader> 如何使用 <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> 方法处理两个 SELECT 语句的结果。  
  
 [!code-csharp[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/VB/source.vb#1)]  
  
## 从 DataReader 中获取架构信息  
 当 **DataReader** 打开时，可以使用 **GetSchemaTable** 方法检索有关当前结果集的架构信息。  **GetSchemaTable** 将返回一个填充了行和列的 <xref:System.Data.DataTable> 对象，这些行和列包含当前结果集的架构信息。  对于结果集的每一列，**DataTable** 都包含一行。  架构表行的每一列都映射到在结果集中返回的列的属性，其中 **ColumnName** 是属性的名称，而列的值为属性的值。  以下代码示例为 **DataReader** 编写架构信息。  
  
 [!code-csharp[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/VB/source.vb#1)]  
  
## 使用 OLE DB 章节  
 分层行集或章节（OLE DB 类型 **DBTYPE\_HCHAPTER**、ADO 类型 **adChapter**）可以使用 <xref:System.Data.OleDb.OleDbDataReader> 来检索。  当以 **DataReader** 的形式返回包含某章节的查询时，该章节将以此 **DataReader** 中列的形式返回，并作为 **DataReader** 对象公开。  
  
 ADO.NET **DataSet** 也可用于通过表间的父子关系来表示分层行集。  有关详细信息，请参阅[DataSet、DataTable 和 DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)。  
  
 以下代码示例使用 MSDataShape 提供程序来为客户列表中的每个客户生成订单的章节列。  
  
```vb  
Using connection As OleDbConnection = New OleDbConnection( _  
  "Provider=MSDataShape;Data Provider=SQLOLEDB;" & _  
  "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind")  
  
Dim custCMD As OleDbCommand = New OleDbCommand( _  
  "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " & _  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " & _  
  "RELATE CustomerID TO CustomerID)", connection)  
connection.Open()  
  
Dim custReader As OleDbDataReader = custCMD.ExecuteReader()  
Dim orderReader As OleDbDataReader  
  
Do While custReader.Read()  
  Console.WriteLine("Orders for " & custReader.GetString(1))   
  ' custReader.GetString(1) = CompanyName  
  
  orderReader = custReader.GetValue(2)  
  ' custReader.GetValue(2) = Orders chapter as DataReader  
  
  Do While orderReader.Read()  
    Console.WriteLine(vbTab & orderReader.GetInt32(1))  
    ' orderReader.GetInt32(1) = OrderID  
  Loop  
  orderReader.Close()  
Loop  
' Make sure to always close readers and connections.  
custReader.Close()  
End Using  
```  
  
```csharp  
Using (OleDbConnection connection = new OleDbConnection(  
  "Provider=MSDataShape;Data Provider=SQLOLEDB;" +  
  "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind"));  
{  
OleDbCommand custCMD = new OleDbCommand(  
  "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " +  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " +  
  "RELATE CustomerID TO CustomerID)", connection);  
connection.Open();  
  
OleDbDataReader custReader = custCMD.ExecuteReader();  
OleDbDataReader orderReader;  
  
while (custReader.Read())  
{  
  Console.WriteLine("Orders for " + custReader.GetString(1));   
  // custReader.GetString(1) = CompanyName  
  
  orderReader = (OleDbDataReader)custReader.GetValue(2);        
  // custReader.GetValue(2) = Orders chapter as DataReader  
  
  while (orderReader.Read())  
    Console.WriteLine("\t" + orderReader.GetInt32(1));          
    // orderReader.GetInt32(1) = OrderID  
  orderReader.Close();  
}  
// Make sure to always close readers and connections.  
custReader.Close();  
}  
```  
  
## 使用 Oracle REF CURSOR 返回结果  
 Oracle .NET Framework 数据提供程序支持使用 Oracle REF CURSOR 返回查询结果。  Oracle REF CURSOR 以 <xref:System.Data.OracleClient.OracleDataReader> 的形式返回。  
  
 可以使用 <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A> 方法检索表示 Oracle REF CURSOR 的 **OracleDataReader** 对象，也可以将返回一个或多个 Oracle REF CURSOR 的 <xref:System.Data.OracleClient.OracleCommand> 指定为用于填充 <xref:System.Data.DataSet> 的 <xref:System.Data.OracleClient.OracleDataAdapter> 的 **SelectCommand**。  
  
 若要访问从 Oracle 数据源中返回的 REF CURSOR，请为查询创建 **OracleCommand**，并将引用 REF CURSOR 的输出参数添加到 **OracleCommand** 的 **Parameters** 集合中。  该参数的名称必须与查询中的 REF CURSOR 参数名称相匹配。  将参数类型设置为 **OracleType.Cursor**。  **OracleCommand** 的 **ExecuteReader** 方法将为 REF CURSOR 返回 **OracleDataReader**。  
  
 如果 **OracleCommand** 返回多个 REF CURSOR，则将添加多个输出参数。  通过调用 **OracleCommand.ExecuteReader** 方法可以访问不同的 REF CURSOR。  调用 **ExecuteReader** 将返回引用第一个 REF CURSOR 的 **OracleDataReader**。  然后，可以调用 **OracleDataReader.NextResult** 方法访问随后的 REF CURSOR。  尽管 **OracleCommand.Parameters** 集合中参数的名称与 REF CURSOR 输出参数名称相匹配，但 **OracleDataReader** 将按这些参数添加到 **Parameters** 集合中的顺序进行访问。  
  
 例如，请看下面这个 Oracle 包和包正文。  
  
```  
CREATE OR REPLACE PACKAGE CURSPKG AS   
  TYPE T_CURSOR IS REF CURSOR;   
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,   
    DEPTCURSOR OUT T_CURSOR);   
END CURSPKG;  
  
CREATE OR REPLACE PACKAGE BODY CURSPKG AS   
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,   
    DEPTCURSOR OUT T_CURSOR)   
  IS   
  BEGIN   
    OPEN EMPCURSOR FOR SELECT * FROM DEMO.EMPLOYEE;   
    OPEN DEPTCURSOR FOR SELECT * FROM DEMO.DEPARTMENT;   
  END OPEN_TWO_CURSORS;   
END CURSPKG;   
```  
  
 以下代码将创建从先前的 Oracle 包返回 REF CURSOR 的 **OracleCommand**，方法是将类型 **OracleType.Cursor** 的两个参数添加到 **Parameters** 集合中。  
  
```vb  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
```  
  
```csharp  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
```  
  
 以下代码使用 **OracleDataReader** 的 **Read** 和 **NextResult** 方法返回先前命令的结果。  REF CURSOR 参数按顺序返回。  
  
```vb  
oraConn.Open()  
  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.CommandType = CommandType.StoredProcedure  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
  
Dim reader As OracleDataReader = cursCmd.ExecuteReader()  
  
Console.WriteLine(vbCrLf & "Emp ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2))  
Loop  
  
reader.NextResult()  
  
Console.WriteLine(vbCrLf & "Dept ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}", reader.GetOracleNumber(0), reader.GetString(1))  
Loop  
' Make sure to always close readers and connections.  
reader.Close()  
oraConn.Close()  
```  
  
```csharp  
oraConn.Open();  
  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.CommandType = CommandType.StoredProcedure;  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
  
OracleDataReader reader = cursCmd.ExecuteReader();  
  
Console.WriteLine("\nEmp ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2));  
  
reader.NextResult();  
  
Console.WriteLine("\nDept ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}", reader.GetOracleNumber(0), reader.GetString(1));  
// Make sure to always close readers and connections.  
reader.Close();  
oraConn.Close();  
```  
  
 以下示例使用先前的命令用 Oracle 包的结果来填充 **DataSet**。  
  
> [!NOTE]
>  为了避免 **OverflowException**，建议您在将值存储在 **DataRow** 中之前，还应执行从 Oracle NUMBER 类型到有效的 .NET Framework 类型的任何转换。  可以使用 **FillError** 事件来确定是否发生了 **OverflowException**。  有关 **FillError** 事件的更多信息，请参见 [处理 DataAdapter 事件](../../../../docs/framework/data/adonet/handling-dataadapter-events.md)。  
  
```vb  
Dim ds As DataSet = New DataSet()  
  
Dim adapter As OracleDataAdapter = New OracleDataAdapter(cursCmd)  
adapter.TableMappings.Add("Table", "Employees")  
adapter.TableMappings.Add("Table1", "Departments")  
  
adapter.Fill(ds)  
```  
  
```csharp  
DataSet ds = new DataSet();  
  
OracleDataAdapter adapter = new OracleDataAdapter(cursCmd);  
adapter.TableMappings.Add("Table", "Employees");  
adapter.TableMappings.Add("Table1", "Departments");  
  
adapter.Fill(ds);  
```  
  
## 请参阅  
 [Working with DataReaders](http://msdn.microsoft.com/zh-cn/126a966a-d08d-4d22-a19f-f432908b2b54)   
 [DataAdapter 和 DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [命令和参数](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [检索数据库架构信息](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)