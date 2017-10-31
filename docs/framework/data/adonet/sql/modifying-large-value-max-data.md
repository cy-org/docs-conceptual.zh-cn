---
title: "在 ADO.NET 中修改大值 (max) 数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8aca5f00-d80e-4320-81b3-016d0466f7ee
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 在 ADO.NET 中修改大值 (max) 数据
大型对象 \(LOB\) 数据类型是那些超过 8 千字节 \(KB\) 最大行大小的数据类型。  SQL Server 为 `varchar`、`nvarchar` 和 `varbinary` 数据类型提供了 `max` 说明符以允许存储最大为 2^32 字节的值。  表列和 Transact\-SQL 变量可以指定 `varchar(max)`、`nvarchar(max)` 或 `varbinary(max)` 数据类型。  在 ADO.NET 中，`max` 数据类型可通过 `DataReader` 来获取，并可指定为输入和输出参数值而无需任何特殊处理。  对于大型 `varchar` 数据类型，可以增量检索和更新数据。  
  
 可以使用 `max` 数据类型进行比较（作为 Transact\-SQL 变量）和进行串联。  它们还可以用于 SELECT 语句的 DISTINCT、ORDER BY、GROUP BY 子句中，以及用于聚合、联接和子查询中。  
  
 下表提供指向 SQL Server 联机丛书中的文档的链接。  
  
 **SQL Server 联机丛书**  
  
1.  [使用大值数据类型](http://go.microsoft.com/fwlink/?LinkId=120498)（可能为英文网页）  
  
## 大值类型限制  
 下面的限制适用于 `max` 数据类型，但对于较小的数据类型则不存在此限制：  
  
-   `sql_variant` 不能包含大型 `varchar` 数据类型。  
  
-   大型 `varchar` 列不能指定为索引中的键列。  它们可以存在于非聚集索引中包含的列中。  
  
-   大型 `varchar` 列不能用作分区键列。  
  
## 在 Transact\-SQL 中使用大值类型  
 Transact\-SQL `OPENROWSET` 函数是一个用于连接和访问远程数据的一次性方法。  它包含从 OLE DB 数据源访问远程数据所需的所有连接信息。  可以在某一查询的 FROM 子句中像表名称一样引用 `OPENROWSET`。  根据 OLE DB 提供程序的功能，它还可作为 INSERT、UPDATE 或 DELETE 语句的目标表被引用。  
  
 `OPENROWSET` 功能包含 `BULK` 行集提供程序，通过此提供程序，您可以直接从文件读取数据而不必将数据加载到目标表  这使您可以在简单的 INSERT SELECT 语句中使用 `OPENROWSET`。  
  
 `OPENROWSET`  `BULK` 选项参数可以有效地控制在何处开始和结束读取数据、如何处理错误以及如何解释数据。  例如，可以指定将数据文件作为 `varbinary`、`varchar` 或 `nvarchar` 类型的单行单列行集合进行读取。  有关完整语法和选项，请参见 SQL Server 联机图书。  
  
 下面的示例将一幅照片插入 AdventureWorks 示例数据库的 ProductPhoto 表中。  在使用 `BULK``OPENROWSET` 提供程序时，即使不将值插入每个列中，也必须提供列的命名列表。  在本例中，主键定义为标识列，并可从列的列表中省略。  请注意，您还必须在 `OPENROWSET` 语句的末尾提供一个相关名称，在本例中该名称是 ThumbnailPhoto。  该名称与文件要加载到的 `ProductPhoto` 表中的列关联。  
  
```  
INSERT Production.ProductPhoto (  
    ThumbnailPhoto,   
    ThumbnailPhotoFilePath,   
    LargePhoto,   
    LargePhotoFilePath)  
SELECT ThumbnailPhoto.*, null, null, N'tricycle_pink.gif'  
FROM OPENROWSET   
    (BULK 'c:\images\tricycle.jpg', SINGLE_BLOB) ThumbnailPhoto  
```  
  
## 使用 UPDATE .WRITE 更新数据  
 Transact\-SQL UPDATE 语句具有新的 WRITE 语法，用于修改 `varchar(max)`、`nvarchar(max)` 或 `varbinary(max)` 列的内容。  它允许您对数据执行部分更新。  此处所示的 UPDATE .WRITE 语法为缩写形式：  
  
 UPDATE  
  
 { *\<object\>* }  
  
 SET  
  
 { *column\_name* \= { .WRITE \( *expression* , @Offset , @Length \) }  
  
 WRITE 方法指定将修改 *column\_name* 值的某个部分。  表达式是将复制到 *column\_name* 的值，`@Offset` 是将写入表达式的开始点，`@Length` 参数是列中该部分的长度。  
  
|如果|Then|  
|--------|----------|  
|表达式设置为 NULL|忽略 `@Length`，并在指定的 `@Offset` 处截断 *column\_name* 中的值。|  
|`@Offset` 为 NULL|更新操作将表达式追加到现有 *column\_name* 值的末尾并忽略 `@Length`。|  
|`@Offset` 大于 column\_name 值的长度|SQL Server 返回一个错误。|  
|`@Length` 为 NULL|更新操作移除从 `@Offset` 到 `column_name` 值末尾的所有数据。|  
  
> [!NOTE]
>  `@Offset` 和 `@Length` 都不能是负数。  
  
## 示例  
 此 Transact\-SQL 示例更新 DocumentSummary（AdventureWorks 数据库的 Document 表中的 `nvarchar(max)` 列）中的部分值。  通过指定替换单词、现有数据中要替换的单词的开始位置（偏移量）以及要替换的字符数（长度），单词“components”将被替换为“features”。  该示例在 UPDATE 语句之前和之后都包含 SELECT 语句以便比较结果。  
  
```  
USE AdventureWorks;  
GO  
--View the existing value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety components of your bicycle.  
  
--Modify a single word in the DocumentSummary column  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
WHERE DocumentID = 3 ;  
GO   
--View the modified value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety features of your bicycle.  
```  
  
## 在 ADO.NET 中使用大值类型  
 通过将大值类型指定为 <xref:System.Data.SqlClient.SqlDataReader> 中的 <xref:System.Data.SqlClient.SqlParameter> `` 对象以返回结果集，或者通过使用 <xref:System.Data.SqlClient.SqlDataAdapter> 来填充 `DataSet`\/`DataTable`，您可以在 ADO.NET 中使用大值类型。  使用大值类型的方式和使用其相关的较小值数据类型的方式之间没有什么不同。  
  
### 使用 GetSqlBytes 检索数据  
 <xref:System.Data.SqlClient.SqlDataReader> 的 `GetSqlBytes` 方法可用于检索 `varbinary(max)` 列的内容。  下面的代码段假定一个名为 `cmd` 的 <xref:System.Data.SqlClient.SqlCommand> 对象（该对象可从表中选择 `varbinary(max)` 数据）和一个名为 `reader` 的 <xref:System.Data.SqlClient.SqlDataReader> 对象（该对象可将该数据检索为 <xref:System.Data.SqlTypes.SqlBytes>）。  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim bytes As SqlBytes = reader.GetSqlBytes(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBytes bytes = reader.GetSqlBytes(0);  
    }  
```  
  
### 使用 GetSqlChars 检索数据  
 <xref:System.Data.SqlClient.SqlDataReader> 的 `GetSqlChars` 方法可用于检索 `varchar(max)` 或 `nvarchar(max)` 列的内容。  下面的代码段假定一个名为 `cmd` 的 <xref:System.Data.SqlClient.SqlCommand> 对象（该对象可从表中选择 `nvarchar(max)` 数据）和一个名为 `reader` 的 <xref:System.Data.SqlClient.SqlDataReader> 对象（该对象可检索该数据）。  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim buffer As SqlChars = reader.GetSqlChars(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
{  
    SqlChars buffer = reader.GetSqlChars(0);  
}  
```  
  
### 使用 GetSqlBinary 检索数据  
 <xref:System.Data.SqlClient.SqlDataReader> 的 `GetSqlBinary` 方法可用于检索 `varbinary(max)` 列的内容。  下面的代码段假定一个名为 `cmd` 的 <xref:System.Data.SqlClient.SqlCommand> 对象（该对象可从表中选择 `varbinary(max)` 数据）和一个名为 `reader` 的 <xref:System.Data.SqlClient.SqlDataReader> 对象（该对象可将该数据检索为 <xref:System.Data.SqlTypes.SqlBinary> 流）。  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim binaryStream As SqlBinary = reader.GetSqlBinary(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBinary binaryStream = reader.GetSqlBinary(0);  
    }  
```  
  
### 使用 GetBytes 检索数据  
 <xref:System.Data.SqlClient.SqlDataReader> 的 `GetBytes` 方法将从指定列偏移量开始的字节流读入到数组中从指定数组偏移量开始的位置。  下面的代码段假定一个名为 `reader` 的 <xref:System.Data.SqlClient.SqlDataReader> 对象，该对象可将字节检索到字节数组中。  请注意，与 `GetSqlBytes` 不同，`GetBytes` 要求指定数组缓冲区的大小。  
  
```vb  
While reader.Read()  
    Dim buffer(4000) As Byte  
    Dim byteCount As Integer = _  
    CInt(reader.GetBytes(1, 0, buffer, 0, 4000))  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
    byte[] buffer = new byte[4000];  
    long byteCount = reader.GetBytes(1, 0, buffer, 0, 4000);  
}  
```  
  
### 使用 GetValue 检索数据  
 <xref:System.Data.SqlClient.SqlDataReader> 的 `GetValue` 方法将指定列偏移量处的值读入数组。  下面的代码段假定一个名为 `reader` 的 <xref:System.Data.SqlClient.SqlDataReader> 对象，该对象检索第一个列偏移量处的二进制数据，然后检索第二个列偏移量处的字符串数据。  
  
```vb  
While reader.Read()  
    ' Read the data from varbinary(max) column  
    Dim binaryData() As Byte = CByte(reader.GetValue(0))  
  
    ' Read the data from varchar(max) or nvarchar(max) column  
    Dim stringData() As String = Cstr((reader.GetValue(1))  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
    // Read the data from varbinary(max) column  
    byte[] binaryData = (byte[])reader.GetValue(0);  
  
    // Read the data from varchar(max) or nvarchar(max) column  
    String stringData = (String)reader.GetValue(1);  
}  
```  
  
## 从大值类型转换为 CLR 类型  
 可以使用任何字符串转换方法（例如 `ToString`）来转换 `varchar(max)` 或 `nvarchar(max)` 列的内容。  下面的代码段假定一个可检索数据的名为 `reader` 的 <xref:System.Data.SqlClient.SqlDataReader> 对象。  
  
```vb  
While reader.Read()  
    Dim str as String = reader(0).ToString()  
    Console.WriteLine(str)  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
     string str = reader[0].ToString();  
     Console.WriteLine(str);  
}  
```  
  
### 示例  
 下面的代码检索 `AdventureWorks` 数据库的 `ProductPhoto` 表中的名称和 `LargePhoto` 对象，并将其保存到文件。  编译程序集时需要引用 <xref:System.Drawing> 命名空间。  <xref:System.Data.SqlClient.SqlDataReader> 的 <xref:System.Data.SqlClient.SqlDataReader.GetSqlBytes%2A> 方法返回一个 <xref:System.Data.SqlTypes.SqlBytes> 对象，该对象公开 `Stream` 属性。  代码使用此对象创建新的 `Bitmap` 对象，然后以 Gif`ImageFormat` 格式保存该对象。  
  
 [!code-csharp[DataWorks LargeValueType.Photo#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks LargeValueType.Photo/CS/source.cs#1)]
 [!code-vb[DataWorks LargeValueType.Photo#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks LargeValueType.Photo/VB/source.vb#1)]  
  
## 使用大值类型参数  
 在 <xref:System.Data.SqlClient.SqlParameter> 对象中使用大型值类型的方法与在 <xref:System.Data.SqlClient.SqlParameter> 对象中使用较小值类型的方法相同。  可以将大值类型作为 <xref:System.Data.SqlClient.SqlParameter> `` 值进行检索，如下面的示例所示。  代码假定在 AdventureWorks 示例数据库中存在以下 GetDocumentSummary 存储过程。  该存储过程采用名为 @DocumentID 的输入参数，并在 @DocumentSummary 输出参数中返回 DocumentSummary 列的内容。  
  
```  
CREATE PROCEDURE GetDocumentSummary   
(  
    @DocumentID int,  
    @DocumentSummary nvarchar(MAX) OUTPUT  
)  
AS  
SET NOCOUNT ON  
SELECT  @DocumentSummary=Convert(nvarchar(MAX), DocumentSummary)  
FROM    Production.Document  
WHERE   DocumentID=@DocumentID  
```  
  
### 示例  
 ADO.NET 代码创建 <xref:System.Data.SqlClient.SqlConnection> 和 <xref:System.Data.SqlClient.SqlCommand> 对象，以执行 GetDocumentSummary 存储过程并检索以大值类型存储的文档摘要。  代码为 @DocumentID 输入参数传递一个值，并在控制台窗口显示 @DocumentSummary 输出参数中传回的结果。  
  
 [!code-csharp[DataWorks LargeValueType.Param#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks LargeValueType.Param/CS/source.cs#1)]
 [!code-vb[DataWorks LargeValueType.Param#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks LargeValueType.Param/VB/source.vb#1)]  
  
## 请参阅  
 [SQL Server 二进制和大值数据](../../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)   
 [SQL Server 数据类型映射](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)   
 [ADO.NET 中的 SQL Server 数据操作](../../../../../docs/framework/data/adonet/sql/sql-server-data-operations.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)