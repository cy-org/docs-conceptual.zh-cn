---
title: "事务和批量复制操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 事务和批量复制操作
批量复制操作可以作为独立的操作执行，也可以作为多步事务的一部分执行。  后一种方式使您可以在同一事务中执行多个批量复制操作并执行其他数据库操作（例如插入、更新和删除），同时仍能够提交或回滚整个事务。  
  
 默认情况下，批量复制操作作为独立的操作执行。  批量复制操作以非事务性方式发生，不可能使其回滚。  如果需要在出错时回滚全部批量复制或它的一部分，可以使用 <xref:System.Data.SqlClient.SqlBulkCopy> 托管的事务，在现有事务中执行批量复制操作，或者在 **System.Transactions**<xref:System.Transactions.Transaction> 中登记它。  
  
## 执行非事务性批量复制操作  
 下面的控制台应用程序演示非事务性批量复制操作在执行操作过程中遇到错误时发生的情况。  
  
 在该示例中，源表和目标表分别包括一个名为 **ProductID** 的 `Identity` 列。  代码首先通过删除所有行，然后插入其 **ProductID** 已知存在于源表的单行，准备目标表。  默认情况下，在目标表中为添加的每一行都生成 `Identity` 列的新值。  在此示例中，在打开连接时设置一个选项，该选项强制批量加载进程改为使用来自源表的 `Identity` 值。  
  
 批量复制操作在 <xref:System.Data.SqlClient.SqlBulkCopy.BatchSize%2A> 属性设置为 10 的情况下执行。  当操作遇到无效行时，将引发异常。  在此第一个示例中，批量复制操作是非事务性的。  在错误点之前复制的所有批次都被提交；回滚包含重复键的批次，并且在处理任何其他批次前中止批量复制操作。  
  
> [!NOTE]
>  除非已按照[批量复制示例设置](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)中所述创建了工作表，否则此示例将不会运行。  提供此代码是为了演示仅使用 **SqlBulkCopy** 时的语法。  如果源表和目标表位于同一个 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 实例中，则使用 [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] `INSERT … SELECT` 语句复制数据会更加容易和快速。  
  
 [!code-csharp[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/VB/source.vb#1)]  
  
## 在事务中执行专用的批量复制操作  
 默认情况下，批量复制操作是其自己的事务。  在您要执行专用的批量复制操作时，使用连接字符串创建 <xref:System.Data.SqlClient.SqlBulkCopy> 的新实例，或者在没有活动事务的情况下使用现有 <xref:System.Data.SqlClient.SqlConnection> 对象。  在每一种情况中，批量复制操作都创建该事务，然后提交或回滚该事务。  
  
 您可以在 <xref:System.Data.SqlClient.SqlBulkCopy> 类构造函数中显式指定 <xref:System.Data.SqlClient.SqlBulkCopyOptions> 选项，以显式导致批量复制操作在其自己的事务中执行，使每批批量复制操作都在单独的事务中执行。  
  
> [!NOTE]
>  由于不同批次在不同事务中执行，因此，如果在批量复制操作期间发生错误，则当前批次中的所有行都将被回滚，但以前批次中的行将保留在数据库中。  
  
 下面的控制台应用程序与前面的示例相似，只有一个例外：在此示例中，批量复制操作管理自己的事务。  在错误点之前复制的所有批次都被提交；回滚包含重复键的批次，并且在处理任何其他批次前中止批量复制操作。  
  
> [!IMPORTANT]
>  除非已按照[批量复制示例设置](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)中所述创建了工作表，否则此示例将不会运行。  提供此代码是为了演示仅使用 **SqlBulkCopy** 时的语法。  如果源表和目标表位于同一个 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 实例中，则使用 [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] `INSERT … SELECT` 语句复制数据会更加容易和快速。  
  
 [!code-csharp[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/VB/source.vb#1)]  
  
## 使用现有事务  
 您可以将现有 <xref:System.Data.SqlClient.SqlTransaction> 对象指定为 <xref:System.Data.SqlClient.SqlBulkCopy> 构造函数中的参数。  在这种情况下，会在现有事务中执行批量复制操作，并且不会对事务状态进行任何更改（这意味着不提交也不中止事务）。  这允许应用程序在具有其他数据库操作的事务中包含批量复制操作。  但是，如果您没有指定 <xref:System.Data.SqlClient.SqlTransaction> 对象并传递空引用，而且连接具有活动的事务，则引发异常。  
  
 如果由于发生错误而需要回滚整个批量复制操作，或者批量复制应作为更大的可回滚进程的一部分执行，则可以将 <xref:System.Data.SqlClient.SqlTransaction> 对象提供给 <xref:System.Data.SqlClient.SqlBulkCopy> 构造函数。  
  
 下面的控制台应用程序与第一个（非事务性）示例相似，但有一个例外：在此示例中，批量复制操作包含在一个更大的外部事务中。  在发生了主键冲突错误时，回滚整个事务并且不会将任何行添加到目标表。  
  
> [!IMPORTANT]
>  除非已按照[批量复制示例设置](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)中所述创建了工作表，否则此示例将不会运行。  提供此代码是为了演示仅使用 **SqlBulkCopy** 时的语法。  如果源表和目标表位于同一个 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 实例中，则使用 [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] `INSERT … SELECT` 语句复制数据会更加容易和快速。  
  
 [!code-csharp[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/VB/source.vb#1)]  
  
## 请参阅  
 [SQL Server 中的批量复制操作](../../../../../docs/framework/data/adonet/sql/bulk-copy-operations-in-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)