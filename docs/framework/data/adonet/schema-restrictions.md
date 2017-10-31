---
title: "架构限制 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 73d2980e-e73c-4987-913a-8ddc93d09144
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 架构限制
**GetSchema** 方法的第二个可选参数是用于限制返回的架构信息量的限制，该参数以字符串数组的形式传递给 **GetSchema** 方法。  在数组中的位置确定可以传递的值，这等效于限制数。  
  
 例如，下表说明使用适用于 SQL Server 的 .NET Framework 数据提供程序时“Tables”架构集合支持的限制。  SQL Server 架构集合的其他限制在本主题的结尾处列出。  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|所有者|@Owner|TABLE\_SCHEMA|2|  
|表|@Name|TABLE\_NAME|3|  
|TableType|@TableType|TABLE\_TYPE|4|  
  
## 指定限制值  
 要使用“Tables”架构集合的一个限制，只需创建一个包含四个元素的字符串数组，然后在与限制数匹配的元素中填充值。  例如，要将 **GetSchema** 方法返回的表限制为仅返回“Sales”架构中的表，将数组的第二个元素设置为“Sales”，然后再将其传递给 **GetSchema** 方法。  
  
> [!NOTE]
>  `SqlClient` 和 `OracleClient` 的限制集合还有附加的 `ParameterName` 列。  为了向后兼容，仍提供限制默认列，但是目前忽略该列。  在指定限制值时，应使用参数化查询（而不是字符串替换）来最大程度地降低受到 SQL 注入式攻击的风险。  
  
> [!NOTE]
>  数组中的元素数必须小于或等于指定架构集合支持的限制数，否则，将引发 <xref:System.ArgumentException>。  可以小于最大限制数。  缺少的限制假定为空（无限制）。  
  
 可以通过调用包含限制架构集合名称“MetaDataCollections”的 **GetSchema** 方法来查询由 .NET Framework 管理的提供程序，以确定支持的限制列表。  此时将返回 <xref:System.Data.DataTable>，包含集合名称、限制名称、默认限制值和限制数的列表。  
  
### 示例  
 以下示例演示如何使用适用于 SQL Server 的 .NET Framework 数据提供程序的 <xref:System.Data.SqlClient.SqlConnection> 类的 <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> 方法来检索与 **AdventureWorks** 示例数据库中包含的所有表有关的架构信息，并将返回的信息仅限于“Sales”中的表：  
  
 \[Visual Basic\]  
  
```  
Imports System.Data.SqlClient  
  
Module Module1  
Sub Main()  
  Dim connectionString As String = _  
    "Data Source=(local);Database=AdventureWorks;" & _  
       "Integrated Security=true;";  
  
  Dim restrictions(3) As String  
  Using connection As New SqlConnection(connectionString)  
    connection.Open()  
  
    'Specify the restrictions.  
    restrictions(1) = "Sales"  
    Dim table As DataTable = connection.GetSchema("Tables", _  
       restrictions)  
  
    ' Display the contents of the table.  
      For Each row As DataRow In table.Rows  
         For Each col As DataColumn In table.Columns  
            Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
         Next  
         Console.WriteLine("============================")  
      Next  
    Console.WriteLine("Press any key to continue.")  
    Console.ReadKey()  
  End Using  
End Sub  
End Module  
```  
  
 \[C\#\]  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
class Program  
{  
  static void Main()  
  {  
    string connectionString =   
       "Data Source=(local);Database=AdventureWorks;" +  
       "Integrated Security=true;";  
    using (SqlConnection connection =  
       new SqlConnection(connectionString))  
    {  
        connection.Open();  
  
        // Specify the restrictions.  
        string[] restrictions = new string[4];  
        restrictions[1] = "Sales";  
        System.Data.DataTable table = connection.GetSchema(  
          "Tables", restrictions);  
  
        // Display the contents of the table.  
        foreach (System.Data.DataRow row in table.Rows)  
        {  
            foreach (System.Data.DataColumn col in table.Columns)  
            {  
                Console.WriteLine("{0} = {1}",   
                  col.ColumnName, row[col]);  
            }  
            Console.WriteLine("============================");  
        }  
        Console.WriteLine("Press any key to continue.");  
        Console.ReadKey();  
    }  
  }  
  
  private static string GetConnectionString()  
  {  
     // To avoid storing the connection string in your code,  
     // you can retrieve it from a configuration file.  
     return "Data Source=(local);Database=AdventureWorks;" +  
        "Integrated Security=true;";  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
     foreach (System.Data.DataRow row in table.Rows)  
     {  
        foreach (System.Data.DataColumn col in table.Columns)  
        {  
           Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
        }  
     Console.WriteLine("============================");  
     }  
  }  
}  
```  
  
## SQL Server 架构限制  
 下表列出了 SQL Server 架构集合的限制。  
  
### Users  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|User\_Name|@Name|name|1|  
  
### 数据库  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|名称|@Name|名称|1|  
  
### 表  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|所有者|@Owner|TABLE\_SCHEMA|2|  
|表|@Name|TABLE\_NAME|3|  
|TableType|@TableType|TABLE\_TYPE|4|  
  
### Columns  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|所有者|@Owner|TABLE\_SCHEMA|2|  
|表|@Table|TABLE\_NAME|3|  
|列|@Column|COLUMN\_NAME|4|  
  
### StructuredTypeMembers  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|所有者|@Owner|TABLE\_SCHEMA|2|  
|表|@Table|TABLE\_NAME|3|  
|列|@Column|COLUMN\_NAME|4|  
  
### 视图  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|所有者|@Owner|TABLE\_SCHEMA|2|  
|表|@Table|TABLE\_NAME|3|  
  
### ViewColumns  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|VIEW\_CATALOG|1|  
|所有者|@Owner|VIEW\_SCHEMA|2|  
|表|@Table|VIEW\_NAME|3|  
|列|@Column|COLUMN\_NAME|4|  
  
### ProcedureParameters  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|SPECIFIC\_CATALOG|1|  
|所有者|@Owner|SPECIFIC\_SCHEMA|2|  
|名称|@Name|SPECIFIC\_NAME|3|  
|参数|@Parameter|PARAMETER\_NAME|4|  
  
### 过程  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|SPECIFIC\_CATALOG|1|  
|所有者|@Owner|SPECIFIC\_SCHEMA|2|  
|名称|@Name|SPECIFIC\_NAME|3|  
|类型|@Type|ROUTINE\_TYPE|4|  
  
### IndexColumns  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|db\_name\(\)|1|  
|所有者|@Owner|user\_name\(\)|2|  
|表|@Table|o.  name|3|  
|ConstraintName|@ConstraintName|x.  name|4|  
|列|@Column|c.  name|5|  
  
### 索引  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|db\_name\(\)|1|  
|所有者|@Owner|user\_name\(\)|2|  
|表|@Table|o.  name|3|  
  
### UserDefinedTypes  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|assembly\_name|@AssemblyName|assemblies.  name|1|  
|udt\_name|@UDTName|types.assembly\_class|2|  
  
### ForeignKeys  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|CONSTRAINT\_CATALOG|1|  
|所有者|@Owner|CONSTRAINT\_SCHEMA|2|  
|表|@Table|TABLE\_NAME|3|  
|名称|@Name|CONSTRAINT\_NAME|4|  
  
## SQL Server 2008  
 下表列出了 SQL Server 2008 架构集合的限制。  这些限制从 .NET Framework 版本 3.5 SP1 和 SQL Server 2008 开始生效。  .NET Framework 和 SQL Server 的早期版本不支持这些限制。  
  
### ColumnSetColumns  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|所有者|@Owner|TABLE\_SCHEMA|2|  
|表|@Table|TABLE\_NAME|3|  
  
### AllColumns  
  
|限制名称|参数名称|限制默认值|限制数|  
|----------|----------|-----------|---------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|所有者|@Owner|TABLE\_SCHEMA|2|  
|表|@Table|TABLE\_NAME|3|  
|列|@Column|COLUMN\_NAME|4|  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)