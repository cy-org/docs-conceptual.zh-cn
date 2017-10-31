---
title: "单次批量复制操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5e7ff0be-3f23-4996-a92c-bd54d65c3836
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 单次批量复制操作
执行 SQL Server 批量复制操作最简单的方法就是对数据库执行单次操作。  默认情况下，批量复制操作是作为一个独立的操作执行的：该复制操作以非事务处理方式进行，不可进行回滚。  
  
> [!NOTE]
>  如果需要在出错时回滚批量复制的全部或部分，可以使用 <xref:System.Data.SqlClient.SqlBulkCopy> 管理的事务，或在现有事务中执行批量复制操作。  如果连接在 **System.Transactions** 事务中（显式或隐式）登记，**SqlBulkCopy** 也将适用于 <xref:System.Transactions>。  
>   
>  有关详细信息，请参阅[事务和批量复制操作](../../../../../docs/framework/data/adonet/sql/transaction-and-bulk-copy-operations.md)。  
  
 执行批量复制操作的一般步骤如下所示：  
  
1.  连接到源服务器上并获取要复制的数据。  如果可以从 <xref:System.Data.IDataReader> 或 <xref:System.Data.DataTable> 对象检索数据，则这些数据还可能来自其他源。  
  
2.  连接到目标服务器（除非您希望 **SqlBulkCopy** 为您建立连接）。  
  
3.  创建一个 <xref:System.Data.SqlClient.SqlBulkCopy> 对象，设置任何必要的属性。  
  
4.  设置 **DestinationTableName** 属性以指示执行批量插入操作的目标表。  
  
5.  调用一个 **WriteToServer** 方法。  
  
6.  可以选择更新属性并根据需要再次调用 **WriteToServer**。  
  
7.  调用 <xref:System.Data.SqlClient.SqlBulkCopy.Close%2A>，或将批量复制操作包装在 `Using` 语句中。  
  
> [!CAUTION]
>  我们建议源列和目标列的数据类型匹配。  如果数据类型不匹配，则 **SqlBulkCopy** 会尝试使用由 <xref:System.Data.SqlClient.SqlParameter.Value%2A> 部署的规则将每个源值转换为目标数据类型。  转换可能会影响性能，还可能会导致意外的错误。  例如，大多数情况下，`Double` 数据类型可以转换为 `Decimal` 数据类型，但是有时就不能。  
  
## 示例  
 以下控制台应用程序演示如何使用 <xref:System.Data.SqlClient.SqlBulkCopy> 类加载数据。  在此示例中，<xref:System.Data.SqlClient.SqlDataReader> 用于将数据从 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] **AdventureWorks** 数据库的 **Production.Product** 表复制到相同数据库的一个类似的表中。  
  
> [!IMPORTANT]
>  除非已按照[批量复制示例设置](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)中所述创建了工作表，否则此示例将不会运行。  提供此代码是为了演示仅使用 **SqlBulkCopy** 时的语法。  如果源表和目标表位于同一个 SQL Server 实例中，则使用 Transact\-SQL `INSERT … SELECT` 语句复制数据会更加容易、更加迅速。  
  
 [!code-csharp[DataWorks BulkCopy.Single#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks BulkCopy.Single/CS/source.cs#1)]
 [!code-vb[DataWorks BulkCopy.Single#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks BulkCopy.Single/VB/source.vb#1)]  
  
## 使用 Transact\-SQL 和命令类执行批量复制操作  
 以下示例说明如何使用 <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> 方法执行 BULK INSERT 语句。  
  
> [!NOTE]
>  数据源的文件路径相对于服务器。  要成功执行批量复制操作，服务器进程必须具有对该路径的访问权限。  
  
```vb  
Using connection As SqlConnection = New SqlConnection(connectionString)  
Dim queryString As String = _  
    "BULK INSERT Northwind.dbo.[Order Details] FROM " & _  
    "'f:\mydata\data.tbl' WITH (FORMATFILE='f:\mydata\data.fmt' )"  
connection.Open()  
SqlCommand command = New SqlCommand(queryString, connection);  
  
command.ExecuteNonQuery()  
End Using  
```  
  
```csharp  
using (SqlConnection connection = New SqlConnection(connectionString))  
{  
string queryString =  "BULK INSERT Northwind.dbo.[Order Details] " +  
    "FROM 'f:\mydata\data.tbl' " +  
    "WITH ( FORMATFILE='f:\mydata\data.fmt' )";  
connection.Open();  
SqlCommand command = new SqlCommand(queryString, connection);  
  
command.ExecuteNonQuery();  
}  
```  
  
## 请参阅  
 [SQL Server 中的批量复制操作](../../../../../docs/framework/data/adonet/sql/bulk-copy-operations-in-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)