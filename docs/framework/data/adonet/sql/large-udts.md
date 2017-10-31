---
title: "大型 UDT | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 420ae24e-762b-4e09-b4c3-2112c470ee49
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 大型 UDT
通过用户定义类型 \(UDT\)，开发人员可通过在 SQL Server 数据库中存储公共语言运行时 \(CLR\) 对象来扩展服务器的标量类型系统。  UDT 可以包含多个元素并可具有多种行为，与传统别名数据类型不同，它们由单一 SQL Server 系统数据类型组成。  
  
> [!NOTE]
>  必须安装 .NET Framework 3.5 SP1（或更高版本）才能利用针对大型 UDT 增强的 SqlClient 支持。  
  
 以前，UDT 的最大大小限制为 8KB。  在 SQL Server 2008 中，对于具有 <xref:Microsoft.SqlServer.Server.Format> 格式的 UDT，此限制已被取消。  
  
 有关用户定义类型的完整文档，请参见与您所使用的 SQL Server 版本对应的 SQL Server 联机丛书。  
  
 **SQL Server 联机丛书**  
  
1.  [CLR 用户定义类型](http://go.microsoft.com/fwlink/?LinkId=98366)（可能为英文网页）  
  
## 使用 GetSchema 检索 UDT 架构  
 <xref:System.Data.SqlClient.SqlConnection> 的 <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> 方法可返回 <xref:System.Data.DataTable> 中的数据库架构信息。  有关详细信息，请参阅[SQL Server 架构集合](../../../../../docs/framework/data/adonet/sql-server-schema-collections.md)。  
  
### UDT 的 GetSchemaTable 列值  
 <xref:System.Data.SqlClient.SqlDataReader> 的 <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> 方法可返回描述列元数据的 <xref:System.Data.DataTable>。  下表介绍了 SQL Server 2005 与 SQL Server 2008 中大型 UDT 的列元数据的差异。  
  
|SqlDataReader 列|SQL Server 2005|SQL Server 2008 及更高版本|  
|---------------------|---------------------|---------------------------|  
|`ColumnSize`|不定|不定|  
|`NumericPrecision`|255|255|  
|`NumericScale`|255|255|  
|`DataType`|`Byte[]`|UDT 实例|  
|`ProviderSpecificDataType`|`SqlTypes.SqlBinary`|UDT 实例|  
|`ProviderType`|21 \(`SqlDbType.VarBinary`\)|29 \(`SqlDbType.Udt`\)|  
|`NonVersionedProviderType`|29 \(`SqlDbType.Udt`\)|29 \(`SqlDbType.Udt`\)|  
|`DataTypeName`|`SqlDbType.VarBinary`|以 *Database.SchemaName.TypeName* 形式指定的由三部分组成的名称。|  
|`IsLong`|不定|不定|  
  
## SqlDataReader 注意事项  
 从 SQL Server 2008 开始，<xref:System.Data.SqlClient.SqlDataReader> 已得到扩展，可支持检索大型 UDT 值。  [SqlDataReader](assetId:///SqlDataReader?qualifyHint=False&amp;autoUpgrade=True) 处理大型 UDT 值的方式取决于您所使用的 SQL Server 版本以及连接字符串中指定的 `Type System Version`。  有关详细信息，请参阅<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>。  
  
 当 `Type System Version` 设置为 SQL Server 2005 时，<xref:System.Data.SqlClient.SqlDataReader> 的以下方法将返回 <xref:System.Data.SqlTypes.SqlBinary> 而不是 UDT：  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  ``  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  ``  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
 当 `Type System Version` 设置为 SQL Server 2005 时，以下方法将返回 `Byte[]` 的数组而不是 UDT：  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetValue%2A>  ``  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
 请注意，不会对 ADO.NET 的当前版本进行任何转换。  
  
## 指定 SqlParameters  
 下面的 <xref:System.Data.SqlClient.SqlParameter> 属性已得到扩展，可以使用大型 UDT。  
  
|SqlParameter 属性|描述|  
|---------------------|--------|  
|<xref:System.Data.SqlClient.SqlParameter.Value%2A>|获取或设置表示参数值的对象。  默认值为 null。  此属性可以是 `SqlBinary`、`Byte[]` 或一个托管对象。|  
|<xref:System.Data.SqlClient.SqlParameter.SqlValue%2A>|获取或设置表示参数值的对象。  默认值为 null。  此属性可以是 `SqlBinary`、`Byte[]` 或一个托管对象。|  
|<xref:System.Data.SqlClient.SqlParameter.Size%2A>|获取或设置要解析的参数值的大小。  默认值为 0。  此属性可以是表示参数值大小的一个整数。  对于大型 UDT，此属性可以是 UDT 的实际大小，也可以是 \-1 以表示未知大小。|  
  
## 检索数据示例  
 下面的代码段演示如何检索大型 UDT 数据。  `connectionString` 变量假定已与 SQL Server 数据库建立有效的连接，`commandString` 变量假定存在首先列出主键列的有效 SELECT 语句。  
  
```csharp  
using (SqlConnection connection = new SqlConnection(   
    connectionString, commandString))  
{  
  connection.Open();  
  SqlCommand command = new SqlCommand(commandString);  
  SqlDataReader reader = command.ExecuteReader();  
  while (reader.Read())  
  {  
    // Retrieve the value of the Primary Key column.  
    int id = reader.GetInt32(0);  
  
    // Retrieve the value of the UDT.  
    LargeUDT udt = (LargeUDT)reader[1];  
  
    // You can also use GetSqlValue and GetValue.  
    // LargeUDT udt = (LargeUDT)reader.GetSqlValue(1);  
    // LargeUDT udt = (LargeUDT)reader.GetValue(1);  
  
    Console.WriteLine(  
     "ID={0} LargeUDT={1}", id, udt);  
  }  
reader.close  
}  
```  
  
```vb  
Using connection As New SqlConnection( _  
    connectionString, commandString)  
    connection.Open()  
    Dim command As New SqlCommand(commandString, connection)  
    Dim reader As SqlDataReader  
    reader = command.ExecuteReader  
  
    While reader.Read()  
      ' Retrieve the value of the Primary Key column.  
      Dim id As Int32 = reader.GetInt32(0)  
  
      ' Retrieve the value of the UDT.  
      Dim udt As LargeUDT = CType(reader(1), LargeUDT)  
  
     ' You can also use GetSqlValue and GetValue.  
     ' Dim udt As LargeUDT = CType(reader.GetSqlValue(1), LargeUDT)  
     ' Dim udt As LargeUDT = CType(reader.GetValue(1), LargeUDT)  
  
      ' Print values.  
      Console.WriteLine("ID={0} LargeUDT={1}", id, udt)  
    End While  
    reader.Close()  
End Using  
  
```  
  
## 请参阅  
 [配置参数和参数数据类型](../../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)   
 [检索数据库架构信息](../../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)   
 [SQL Server 数据类型映射](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)   
 [SQL Server 二进制和大值数据](../../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)