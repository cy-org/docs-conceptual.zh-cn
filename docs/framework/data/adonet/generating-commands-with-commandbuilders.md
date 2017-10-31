---
title: "使用 CommandBuilder 生成命令 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e3fb8b5-373b-4f9e-ab03-a22693df8e91
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 使用 CommandBuilder 生成命令
如果在运行时动态指定 `SelectCommand` 属性（例如，通过接受用户提供的文本命令的查询工具），那么您可能无法在设计时指定适当的 `InsertCommand`、`UpdateCommand` 或 `DeleteCommand`。  如果您的 <xref:System.Data.DataTable> 映射到单个数据库表或者是从单个数据库表中生成的，那么您可以利用 <xref:System.Data.Common.DbCommandBuilder> 对象来自动生成 <xref:System.Data.Common.DbDataAdapter> 的 `DeleteCommand`、`InsertCommand` 和 `UpdateCommand`。  
  
 为了能够自动生成命令，必须设置 `SelectCommand` 属性，这是最低要求。  由 `SelectCommand` 属性检索的表架构确定自动生成的 INSERT、UPDATE 和 DELETE 语句的语法。  
  
 为了返回构造 INSERT、UPDATE 和 DELETE SQL 命令所需的元数据，<xref:System.Data.Common.DbCommandBuilder> 必须执行 `SelectCommand`。  因此，必须额外经历一次到数据源的过程，这可能会降低性能。  若要实现最佳性能，请显式指定命令而不是使用 <xref:System.Data.Common.DbCommandBuilder>。  
  
 `SelectCommand` 还必须至少返回一个主键或唯一列。  如果不存在任何主键和唯一列，则会生成 `InvalidOperation` 异常，并且不会生成命令。  
  
 当与 `DataAdapter` 关联时，<xref:System.Data.Common.DbCommandBuilder> 会自动生成 `DataAdapter` 的 `InsertCommand`、`UpdateCommand` 和 `DeleteCommand` 属性（如果它们为空引用）。  如果某个属性已存在 `Command`，则使用现有 `Command`。  
  
 通过联接两个或更多个表来创建的数据库视图不会被视为单个数据库表。  在这种情况下，您无法使用 <xref:System.Data.Common.DbCommandBuilder> 来自动生成命令；必须显式指定命令。  有关显式设置命令以将对 `DataSet` 的更新解析回数据源的信息，请参见[使用 DataAdapter 更新数据源](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)。  
  
 您可能需要将输出参数映射回 `DataSet` 的更新行。  一项常见的任务是从数据源中检索自动生成的标识字段或时间戳的值。  默认情况下，<xref:System.Data.Common.DbCommandBuilder> 不会将输出参数映射到更新行中的列。  在这种情况下，必须显式指定命令。  有关将自动生成的标识字段映射回插入行的列的示例，请参见[检索“标识”或“自动编号”值](../../../../docs/framework/data/adonet/retrieving-identity-or-autonumber-values.md)。  
  
## 自动生成命令的规则  
 下表显示创建自动生成命令的规则。  
  
|命令|规则|  
|--------|--------|  
|`InsertCommand`|在数据源处为表中所有 <xref:System.Data.DataRow.RowState%2A> 为 <xref:System.Data.DataRowState> 的行插入一行。  插入所有可更新列的值（但是不包括标识、表达式或时间戳等列）。|  
|`UpdateCommand`|在数据源处更新表中所有 `RowState` 为 <xref:System.Data.DataRowState> 的行。  更新所有列的值，不可更新的列除外，例如标识列或表达式列。  更新符合以下条件的所有行：数据源中的列值匹配行的主键列值，并且数据源中的剩余列匹配行的原始值。  有关更多信息，请参见本主题后面的“更新和删除的开放式并发模型”。|  
|`DeleteCommand`|在数据源处删除表中所有 `RowState` 为 <xref:System.Data.DataRowState> 的行。  删除符合以下条件的所有行：列值匹配行的主键列值，并且数据源中的剩余列匹配行的原始值。  有关更多信息，请参见本主题后面的“更新和删除的开放式并发模型”。|  
  
## 更新和删除的开放式并发模型  
 为 UPDATE 和 DELETE 语句自动生成命令的逻辑基于“开放式并发” \-\- 即未锁定记录的编辑功能，其他用户或进程可以随时修改。  由于在从 SELECT 语句中返回某记录之后但在发出 UPDATE 或 DELETE 语句之前，该记录可能已被修改，所以自动生成的 UPDATE 或 DELETE 语句包含一个 WHERE 子句，指定只有在行包含所有原始值并且尚未从数据源中删除时，才会更新该行。  这样做的目的是为了避免覆盖新数据。  当自动生成的 UPDATE 命令试图更新已删除或不包含 <xref:System.Data.DataSet> 中原始值的行时，该命令不会影响任何记录，并且会引发 <xref:System.Data.DBConcurrencyException>。  
  
 如果要使 UPDATE 或 DELETE 在不考虑原始值的情况下完成，必须为 `DataAdapter` 显式设置 `UpdateCommand`，而不依赖自动命令生成。  
  
## 自动命令生成逻辑的限制  
 自动命令生成存在以下限制。  
  
### 仅限于无关表  
 自动命令生成逻辑为独立表生成 INSERT、UPDATE 或 DELETE 语句，而不考虑与数据源中其他表的任何关系。  因此，在调用 `Update` 以提交对参与数据库中外键约束的列的更改时，可能会失败。  若要避免这一异常，请不要使用 <xref:System.Data.Common.DbCommandBuilder> 来更新参与外键约束的列，而应显式地指定用于执行该操作的语句。  
  
### 表名称和列名称  
 如果列名称或表名称包含任何特殊字符（如空格、句点、问号或其他非字母数字字符），则即使这些字符用括号分隔，自动命令生成逻辑也可能会失败。  根据具体提供程序，通过设置 QuotePrefix 和 QuoteSuffix 参数，生成逻辑可以处理空格，但无法转义特殊字符。  支持格式为 *catalog.schema.table* 的完全限定表名。  
  
## 使用 CommandBuilder 自动生成 SQL 语句  
 若要为 `DataAdapter` 自动生成 SQL 语句，请先设置 `DataAdapter` 的 `SelectCommand` 属性，然后创建 `CommandBuilder` 对象，并将该对象指定为 `CommandBuilder` 将自动为其生成 SQL 语句的 `DataAdapter` 的参数。  
  
```vb  
' Assumes that connection is a valid SqlConnection object   
' inside of a Using block.  
Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers", connection)  
Dim builder As SqlCommandBuilder = New SqlCommandBuilder(adapter)  
builder.QuotePrefix = "["  
builder.QuoteSuffix = "]"  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object  
// inside of a using block.  
SqlDataAdapter adapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers", connection);  
SqlCommandBuilder builder = new SqlCommandBuilder(adapter);  
builder.QuotePrefix = "[";  
builder.QuoteSuffix = "]";  
```  
  
## 修改 SelectCommand  
 如果您在自动生成 INSERT、UPDATE 或 DELETE 命令后修改 `SelectCommand` 的 `CommandText`，则可能会发生异常。  如果修改后的 `SelectCommand.CommandText` 包含的架构信息与自动生成 INSERT、UPDATE 或 DELETE 命令时使用的 `SelectCommand.CommandText` 不一致，则以后对 `DataAdapter.Update` 方法的调用可能会试图访问 `SelectCommand` 所引用的当前表中已不存在的列，并且将会引发异常。  
  
 可以通过调用 `CommandBuilder` 的 `RefreshSchema` 方法来刷新由 `CommandBuilder` 用于自动生成命令的架构信息。  
  
 如果您想知道自动生成了哪个命令，可以使用 `CommandBuilder` 对象的 `GetInsertCommand`、`GetUpdateCommand` 和 `GetDeleteCommand` 方法并检查关联命令的 `CommandText` 属性，以获得对自动生成命令的引用。  
  
 以下代码示例向控制台写入已自动生成的更新命令。  
  
```  
Console.WriteLine(builder.GetUpdateCommand().CommandText)  
```  
  
 下面的示例在 `custDS` 数据集中重新创建 `Customers` 表。  然后调用 **RefreshSchema** 方法，使用此新列的信息来刷新自动生成的命令。  
  
```vb  
' Assumes an open SqlConnection and SqlDataAdapter inside of a Using block.  
adapter.SelectCommand.CommandText = _  
  "SELECT CustomerID, ContactName FROM dbo.Customers"  
builder.RefreshSchema()  
  
custDS.Tables.Remove(custDS.Tables("Customers"))  
adapter.Fill(custDS, "Customers")  
```  
  
```csharp  
// Assumes an open SqlConnection and SqlDataAdapter inside of a using block.  
adapter.SelectCommand.CommandText =   
  "SELECT CustomerID, ContactName FROM dbo.Customers";  
builder.RefreshSchema();  
  
custDS.Tables.Remove(custDS.Tables["Customers"]);  
adapter.Fill(custDS, "Customers");  
```  
  
## 请参阅  
 [命令和参数](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [执行命令](../../../../docs/framework/data/adonet/executing-a-command.md)   
 [DbConnection、DbCommand 和 DbException](../../../../docs/framework/data/adonet/dbconnection-dbcommand-and-dbexception.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)