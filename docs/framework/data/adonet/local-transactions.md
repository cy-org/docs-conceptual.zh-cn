---
title: "本地事务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ae3712f-ef5e-41a1-9ea9-b3d0399439f1
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 本地事务
如果要将多项任务绑定在一起，使其作为单个工作单元来执行，可以使用 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 中的事务。  例如，假设应用程序执行两个任务。  首先使用订单信息更新表。  然后更新包含库存信息的表，将已订购的商品记入借方。  如果任何一项任务失败，两个更新均将回滚。  
  
## 确定事务类型  
 事务如果是单阶段事务，并且由数据库直接处理，则属于本地事务。  事务如果由事务监视程序进行协调并使用故障保护机制（例如两阶段提交）解决事务，则属于分布式事务。  
  
 每个 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序使用自己的 `Transaction` 对象来执行本地事务。  如果要求事务在 SQL Server 数据库中执行，则选择 <xref:System.Data.SqlClient> 事务。  对于 Oracle 事务，使用 <xref:System.Data.OracleClient> 提供程序。  此外，还提供了一个新的 <xref:System.Data.Common.DbTransaction> 类，用于编写需要事务并且与提供程序无关的代码。  
  
> [!NOTE]
>  在服务器上执行时，事务最有效。  如果使用的 SQL Server 数据库广泛使用显式事务，应考虑使用 Transact\-SQL BEGIN TRANSACTION 语句以存储过程的形式编写这些事务。  有关执行服务器端事务的更多信息，请参见“SQL Server 联机图书”。  
  
## 使用单个连接执行事务  
 在 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 中，使用 `Connection` 对象控制事务。  可以使用 `BeginTransaction` 方法启动本地事务。  开始事务后，可以使用 `Command` 对象的 `Transaction` 属性在该事务中登记一个命令。  然后，可以根据事务组件的成功或失败，提交或回滚在数据源上进行的修改。  
  
> [!NOTE]
>  不应对本地事务使用 `EnlistDistributedTransaction` 方法。  
  
 事务的作用域限于该连接。  以下示例执行显式事务，该事务由 `try` 块中两个独立的命令组成。  这两个命令对 AdventureWorks [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 示例数据库的 Production.ScrapReason 表执行 INSERT 语句，如果没有引发异常，则提交。  如果引发异常，`catch` 块中的代码将回滚事务。  如果在事务完成之前事务中止或连接关闭，事务将自动回滚。  
  
## 示例  
 按照下列步骤执行事务。  
  
1.  调用 <xref:System.Data.SqlClient.SqlConnection> 对象的 <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> 方法，以标记事务的开始。  <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> 方法返回对事务的引用。  此引用分配给在事务中登记的 <xref:System.Data.SqlClient.SqlCommand> 对象。  
  
2.  将 `Transaction` 对象分配给要执行的 <xref:System.Data.SqlClient.SqlCommand> 的 <xref:System.Data.SqlClient.SqlCommand.Transaction%2A> 属性。  如果在具有活动事务的连接上执行命令，并且尚未将 `Transaction` 对象配给 `Command` 对象的 `Transaction` 属性，则会引发异常。  
  
3.  执行所需的命令。  
  
4.  调用 <xref:System.Data.SqlClient.SqlTransaction> 对象的 <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> 方法完成事务，或调用 <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> 方法结束事务。  如果在 <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> 或 <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> 方法执行之前连接关闭或断开，事务将回滚。  
  
 以下代码示例演示对 Microsoft SQL Server 使用 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 的事务逻辑。  
  
 [!code-csharp[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/VB/source.vb#1)]  
  
## 请参阅  
 [事务和并发](../../../../docs/framework/data/adonet/transactions-and-concurrency.md)   
 [分布式事务](../../../../docs/framework/data/adonet/distributed-transactions.md)   
 [System.Transactions 与 SQL Server 的集成](../../../../docs/framework/data/adonet/system-transactions-integration-with-sql-server.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)