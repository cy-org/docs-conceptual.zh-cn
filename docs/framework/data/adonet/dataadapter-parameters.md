---
title: "DataAdapter 参数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f21e6aba-b76d-46ad-a83e-2ad8e0af1e12
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# DataAdapter 参数
<xref:System.Data.Common.DbDataAdapter> 具有四个用于从数据源检索数据和更新数据源中数据的属性：<xref:System.Data.Common.DbDataAdapter.SelectCommand%2A> 属性返回数据源中的数据；<xref:System.Data.Common.DbDataAdapter.InsertCommand%2A>、<xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> 和 <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> 属性用于管理数据源中的更改。  调用 `DataAdapter` 的 `Fill` 方法之前必须设置 `SelectCommand` 属性。  在调用 `DataAdapter` 的 `Update` 方法之前必须设置 `InsertCommand`、`UpdateCommand` 或 `DeleteCommand` 属性，具体取决于对 <xref:System.Data.DataTable> 中的数据做了哪些更改。  例如，如果已添加行，在调用 `Update` 之前必须设置 `InsertCommand`。  当 `Update` 正在处理已插入、已更新或已删除的行时，`DataAdapter` 将使用相应的 `Command` 属性来处理该操作。  有关已修改行的当前信息将通过 `Parameters` 集合传递到 `Command` 对象。  
  
 当更新数据源中的行时，将调用 UPDATE 语句，该语句使用唯一标识符来标识该表中要更新的行。  该唯一标识符通常是主键字段的值。  UPDATE 语句使用的参数既包含唯一标识符又包含要更新的列和值，如下面的 Transact\-SQL 语句所示。  
  
```  
UPDATE Customers SET CompanyName = @CompanyName   
  WHERE CustomerID = @CustomerID  
```  
  
> [!NOTE]
>  参数占位符的语法取决于数据源。  此示例显示 SQL Server 数据源的占位符。  使用问号 \(?\) 占位符代表 <xref:System.Data.OleDb> 和 <xref:System.Data.Odbc> 参数。  
  
 在此 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 示例中，`CompanyName` 字段使用 `CustomerID` 等于 `@CustomerID```参数值的行中的 `@CompanyName` 参数值来进行更新。  这些参数使用 <xref:System.Data.SqlClient.SqlParameter> 对象的 <xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A> 属性从已修改的行中检索相关信息。  下面是上一示例 UPDATE 语句的参数。  代码假定变量 `adapter` 表示有效的 <xref:System.Data.SqlClient.SqlDataAdapter> 对象。  
  
```  
adapter.Parameters.Add( _  
  "@CompanyName", SqlDbType.NChar, 15, "CompanyName")  
Dim parameter As SqlParameter = _  
  adapter.UpdateCommand.Parameters.Add("@CustomerID", _  
  SqlDbType.NChar, 5, "CustomerID")  
parameter.SourceVersion = DataRowVersion.Original  
```  
  
 `Parameters` 集合的 `Add` 方法接受参数的名称、数据类型、大小（如果适用于该类型）以及 `DataTable` 中的 <xref:System.Data.Common.DbParameter.SourceColumn%2A> 的名称。  请注意，`@CustomerID` 参数的 <xref:System.Data.Common.DbParameter.SourceVersion%2A> 设置为 `Original`。  这样可以保证，如果标识列的值已经在修改后的 <xref:System.Data.DataRow> 中被更改，就一定会更新数据源中的现有行。  在这种情况下，`Original` 行值将匹配数据源中的当前值，而 `Current` 行值将包含更新的值。  没有设置 `@CompanyName` 参数的 `SourceVersion`，而将使用默认的 `Current` 行值。  
  
> [!NOTE]
>  对于 `DataAdapter` 的 `Fill` 操作和 `DataReader` 的 `Get` 方法，都将从 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序中返回的类型来推断 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型。  推断的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型和 Microsoft SQL Server、OLE DB 和 ODBC 数据类型的访问器方法在 [ADO.NET 中的数据类型映射](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md) 中说明。  
  
## Parameter.SourceColumn，Parameter.SourceVersion  
 `SourceColumn` 和 `SourceVersion` 可以作为参数传递给 `Parameter` 构造函数，也可以设置为现有 `Parameter` 的属性。  `SourceColumn` 是将要从中检索 `Parameter` 值的 <xref:System.Data.DataRow> 中的 <xref:System.Data.DataColumn> 的名称。  `SourceVersion` 指定 `DataAdapter` 用于检索该值的 `DataRow` 版本。  
  
 下表显示可以与 `SourceVersion` 一起使用的 <xref:System.Data.DataRowVersion> 枚举值。  
  
|DataRowVersion 枚举|描述|  
|-----------------------|--------|  
|`Current`|该参数使用列的当前值。  这是默认设置。|  
|`Default`|该参数使用列的 `DefaultValue`。|  
|`Original`|该参数使用列的原始值。|  
|`Proposed`|该参数使用建议值。|  
  
 下一节中的 `SqlClient` 代码示例为 <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> 定义了一个参数，在该示例中 `CustomerID` 列用作以下两个参数的 `SourceColumn`：`@CustomerID` \(`SET CustomerID = @CustomerID`\) 和 `@OldCustomerID` \(`WHERE CustomerID = @OldCustomerID`\)。  `@CustomerID` 参数用于将 **CustomerID** 列更新为 `DataRow` 中的当前值。  因此，使用 `SourceVersion` 为 `Current` 的 `CustomerID` `SourceColumn`。  *@OldCustomerID* 参数用于标识数据源中的当前行。  由于在该行的 `Original` 版本中找到了匹配列值，所以将使用 `SourceVersion` 为 `Original` 的相同 `SourceColumn` \(`CustomerID`\)。  
  
## 使用 SqlClient 参数  
 下面的示例演示如何创建 <xref:System.Data.SqlClient.SqlDataAdapter> 并将 <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> 设置为 <xref:System.Data.MissingSchemaAction>，以便从数据库中检索其他架构信息。  <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>、<xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>、<xref:System.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> 和 <xref:System.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> 属性集及其相应的 <xref:System.Data.SqlClient.SqlParameter> 对象已添加到 <xref:System.Data.SqlClient.SqlCommand.Parameters%2A> 集合。  该方法返回一个 `SqlDataAdapter` 对象。  
  
 [!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/CS/source.cs#1)]
 [!code-vb[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/VB/source.vb#1)]  
  
## OleDb 参数占位符  
 对于 <xref:System.Data.OleDb.OleDbDataAdapter> 对象和 <xref:System.Data.Odbc.OdbcDataAdapter> 对象，必须使用问号 \(?\) 占位符来标识参数。  
  
```vb  
Dim selectSQL As String = _  
  "SELECT CustomerID, CompanyName FROM Customers " & _  
  "WHERE CountryRegion = ? AND City = ?"  
Dim insertSQL AS String = _  
  "INSERT INTO Customers (CustomerID, CompanyName) VALUES (?, ?)"  
Dim updateSQL AS String = _  
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " & _  
  WHERE CustomerID = ?"  
Dim deleteSQL As String = "DELETE FROM Customers WHERE CustomerID = ?"  
```  
  
```csharp  
string selectSQL =   
  "SELECT CustomerID, CompanyName FROM Customers " +  
  "WHERE CountryRegion = ? AND City = ?";  
string insertSQL =   
  "INSERT INTO Customers (CustomerID, CompanyName) " +  
  "VALUES (?, ?)";  
string updateSQL =   
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " +  
  "WHERE CustomerID = ? ";  
string deleteSQL = "DELETE FROM Customers WHERE CustomerID = ?";  
```  
  
 参数化查询语句定义必须创建的输入和输出参数。  若要创建参数，请使用 `Parameters.Add` 方法或 `Parameter` 构造函数来指定列名称、数据类型和大小。  对于内部数据类型（如 `Integer`）无需包含大小，也可以指定默认大小。  
  
 下面的代码示例创建 SQL 语句的参数，然后填充 `DataSet`。  
  
## OleDb 示例  
  
```vb  
' Assumes that connection is a valid OleDbConnection object.  
Dim adapter As OleDbDataAdapter = New OleDbDataAdapter   
  
Dim selectCMD AS OleDbCommand = New OleDbCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add parameters and set values.  
selectCMD.Parameters.Add( _  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add( _  
  "@City", OleDbType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
  
```  
  
```csharp  
// Assumes that connection is a valid OleDbConnection object.  
OleDbDataAdapter adapter = new OleDbDataAdapter();  
  
OleDbCommand selectCMD = new OleDbCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
// Add parameters and set values.  
selectCMD.Parameters.Add(  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add(  
  "@City", OleDbType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
## Odbc 参数  
  
```vb  
' Assumes that connection is a valid OdbcConnection object.  
Dim adapter As OdbcDataAdapter = New OdbcDataAdapter  
  
Dim selectCMD AS OdbcCommand = New OdbcCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
  
```  
  
```csharp  
// Assumes that connection is a valid OdbcConnection object.  
OdbcDataAdapter adapter = new OdbcDataAdapter();  
  
OdbcCommand selectCMD = new OdbcCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
//Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
> [!NOTE]
>  如果未为参数提供参数名称，则该参数将使用从“Parameter1”开始递增的默认名称 Parameter*N*。  建议在提供参数名称时避免使用 Parameter*N* 命名约定，因为所提供的名称可能会与 `ParameterCollection` 中现有的默认参数名称发生冲突。  如果提供的名称已经存在，将引发异常。  
  
## 请参阅  
 [DataAdapter 和 DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [命令和参数](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [使用 DataAdapter 更新数据源](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)   
 [使用存储过程修改数据](../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)   
 [ADO.NET 中的数据类型映射](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)