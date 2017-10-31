---
title: "SQL Server 中的快照隔离 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 43ae5dd3-50f5-43a8-8d01-e37a61664176
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# SQL Server 中的快照隔离
快照隔离可增强 OLTP 应用程序的并发性。  
  
## 了解快照隔离和行版本控制  
 启用快照隔离之后，每个事务的已更新行版本在 **tempdb** 中维护。  唯一的事务序列号标识每个事务，并且为每个行版本记录这些唯一的编号。  事务使用序列号在事务序列号之前的最新行版本。  事务将忽略在事务开始之后创建的更新的行版本。  
  
 “快照”一词反映的情况是：事务中的所有查询根据事务开始那一刻数据库的状态，看到数据库的相同版本（即快照）。  不会在快照事务中的基础数据行或数据页上获取锁，这样可以执行其他事务，而不会被以前未完成的事务所阻止。  修改数据的事务不会阻止读取数据的事务，读取数据的事务不会阻止写入数据的事务，就好像通常情况下在 SQL Server 中使用默认的 READ COMMITTED 隔离级别一样。  这种无阻止的行为也大大降低了复杂事务出现死锁的可能性。  
  
 快照隔离使用开放式并发模型。  如果快照事务尝试提交对事务开始后更改过的数据的修改，事务将回滚并将引发错误。  对访问要修改的数据的 SELECT 语句使用 UPDLOCK 提示，可以避免此问题。  有关更多信息，请参见“SQL Server 联机图书”中的“锁定提示”。  
  
 在事务中使用快照隔离之前，必须先通过设置 ALLOW\_SNAPSHOT\_ISOLATION ON 数据库选项来启用快照隔离。  这样将激活在临时数据库 \(**tempdb**\) 中存储行版本的机制。  在每个要将快照隔离与 Transact\-SQL ALTER DATABASE 语句一起使用的数据库中，必须启用快照隔离。  从这个方面来说，快照隔离与传统的隔离级别 READ COMMITTED、REPEATABLE READ、SERIALIZABLE 和 READ UNCOMMITTED 不同，这些传统的隔离级别不需要任何配置。  下列语句激活快照隔离，并将默认的 READ COMMITTED 行为替换为 SNAPSHOT：  
  
```  
ALTER DATABASE MyDatabase  
SET ALLOW_SNAPSHOT_ISOLATION ON  
  
ALTER DATABASE MyDatabase  
SET READ_COMMITTED_SNAPSHOT ON  
```  
  
 设置 READ\_COMMITTED\_SNAPSHOT ON 选项后，可以使用默认的 READ COMMITTED 隔离级别访问版本化的行。  如果 READ\_COMMITTED\_SNAPSHOT 选项设置为 OFF，必须为每个会话显式设置 Snapshot 隔离级别，以便访问版本化的行。  
  
## 使用隔离级别管理并发性  
 执行 Transact\-SQL 语句所使用的隔离级别确定其锁定行为和行版本化行为。  隔离级别的作用域为整个连接，使用 SET TRANSACTION ISOLATION LEVEL 语句为连接设置了隔离级别后，在连接关闭或设置了另一个隔离级别之前，该隔离级别将一直生效。  当连接关闭并返回到池时，会保留上一个 SET TRANSACTION ISOLATION LEVEL 语句设置的隔离级别。  重复使用池连接的后续连接会使用连接被汇集时起作用的隔离级别。  
  
 连接中发出的个别查询可包含修改单个语句或事务的隔离，但不会影响该连接的隔离级别的锁提示。  在存储过程或函数中设置的隔离级别或锁提示不会更改调用这些存储过程或函数的连接的隔离级别，并且只在存储过程或函数调用期间生效。  
  
 SQL Server 的早期版本支持 SQL\-92 标准中定义的四个隔离级别：  
  
-   READ UNCOMMITTED 是限制性最弱的隔离级别，因为该级别忽略其他事务放置的锁。  使用 READ UNCOMMITTED 级别执行的事务，可以读取尚未由其他事务提交的修改后的数据值；这些行为称为“脏”读。  
  
-   READ COMMITTED 是 SQL Server 默认的隔离级别。  该级别通过指定语句不能读取其他事务已修改但是尚未提交的数据值，禁止执行脏读。  在当前事务中的各个语句执行之间，其他事务仍可以修改、插入或删除数据，从而产生无法重复的读操作，或“影子”数据。  
  
-   REPEATABLE READ 是比 READ COMMITTED 限制性更强的隔离级别。  该级别包括 READ COMMITTED，并且另外指定了在当前事务提交之前，其他任何事务均不可以修改或删除当前事务已读取的数据。  并发性低于 READ COMMITTED，因为已读数据的共享锁在整个事务期间持有，而不是在每个语句结束时释放。  
  
-   SERIALIZABLE 是限制性最强的隔离级别，因为该级别锁定整个范围的键，并一直持有锁，直到事务完成。  该级别包括 REPEATABLE READ，并增加了在事务完成之前，其他事务不能向事务已读取的范围插入新行的限制。  
  
 有关更多信息，请参见“SQL Server 联机图书”中的“隔离级别”。  
  
### 快照隔离级别扩展  
 SQL Server 通过引入 SNAPSHOT 隔离级别并另外实现 READ COMMITTED 而引入了对 SQL\-92 隔离级别的扩展。  READ\_COMMITTED\_SNAPSHOT 隔离级别可以透明地替换所有事务的 READ COMMITTED。  
  
-   SNAPSHOT 隔离指定在一个事务中读取的数据永远不会反映其他同时进行的事务所作的更改。  事务使用事务开始时存在的数据行版本。  在读取数据时不会对数据放置任何锁，所以，SNAPSHOT 事务不会阻止其他事务写入数据。  写入数据的事务不会阻止快照事务读取数据。  您需要通过设置 ALLOW\_SNAPSHOT\_ISOLATION 数据库选项启用快照隔离后，才可以使用快照隔离。  
  
-   在数据库中启用快照隔离时，READ\_COMMITTED\_SNAPSHOT 数据库选项确定默认 READ COMMITTED 隔离级别的行为。  如果不显式指定 READ\_COMMITTED\_SNAPSHOT ON，READ COMMITTED 将应用于所有隐式事务。  此时的行为与设置 READ\_COMMITTED\_SNAPSHOT OFF（默认设置）相同。  当 READ\_COMMITTED\_SNAPSHOT OFF 生效时，数据库引擎使用共享锁强制使用默认隔离级别。  如果将 READ\_COMMITTED\_SNAPSHOT 数据库选项设置为 ON，数据库引擎将使用行版本化和快照隔离作为默认设置，而不是使用锁来保护数据。  
  
## 快照隔离和行版本化的工作原理  
 启用 SNAPSHOT 隔离级别时，每次更新行时，SQL Server 数据库引擎在 **tempdb** 中存储原始行的副本，并为该行添加事务序列号。  以下是发生的事件序列：  
  
-   新的事务启动，并为该事务分配一个事务序列号。  
  
-   数据库引擎在事务中读取某行，并从 **tempdb** 中检索其序列号与事务序列号最接近并且小于事务序列号的行版本。  
  
-   数据库引擎检查事务编号是否不在未提交事务的事务编号列表中，这些未提交事务是在快照事务开始时进入活动状态的。  
  
-   事务从 **tempdb** 中读取自事务开始以来最新的行版本。  事务不会看到事务开始后插入的新行，因为这些序列号值将大于事务序列号的值。  
  
-   当前事务将看到事务开始后删除的行，因为 **tempdb** 中的行版本具有更低的序列号值。  
  
 快照隔离的实际效果是事务看到在事务开始时存在的所有数据，不会在基础表上授予或放置任何锁。  在存在争用的情况下，这样可以改进性能。  
  
 快照事务始终使用开放式并发控制，不赋予可能阻止其他事务更新行的任何锁。  如果快照事务尝试提交对事务开始后已更改的行的更新，事务将回滚并引发错误。  
  
## 在 ADO.NET 中使用快照隔离  
 ADO.NET 中通过 <xref:System.Data.SqlClient.SqlTransaction> 类支持快照隔离。  如果数据库已启用了快照隔离，但是未配置 READ\_COMMITTED\_SNAPSHOT ON，必须在调用 <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> 方法时，使用 **IsolationLevel.Snapshot** 枚举值启动 <xref:System.Data.SqlClient.SqlTransaction>。  此代码段假定连接是打开的 <xref:System.Data.SqlClient.SqlConnection> 对象。  
  
```vb  
Dim sqlTran As SqlTransaction = _  
  connection.BeginTransaction(IsolationLevel.Snapshot)  
```  
  
```csharp  
SqlTransaction sqlTran =   
  connection.BeginTransaction(IsolationLevel.Snapshot);  
```  
  
### 示例  
 以下示例通过尝试访问锁定的数据，演示不同隔离级别的行为，并非要在生产代码中使用。  
  
 该代码连接到 SQL Server 中的 **AdventureWorks** 示例数据库上，并创建一个名为 **TestSnapshot** 的表，然后插入一行数据。  该代码使用 ALTER DATABASE Transact\-SQL 语句对数据库启用快照隔离，但是不设置 READ\_COMMITTED\_SNAPSHOT 选项，让默认的 READ COMMITTED 隔离级别的行为生效。  然后，该代码执行下列操作：  
  
-   开始但是不完成 sqlTransaction1，sqlTransaction1 使用 SERIALIZABLE 隔离级别开始更新事务。  这样做的结果是锁定表。  
  
-   打开第二个连接，并使用 SNAPSHOT 隔离级别开始第二个事务，读取 **TestSnapshot** 表中的数据。  因为启用了快照隔离，此事务可以读取在开始 sqlTransaction1 之前存在的数据。  
  
-   打开第三个连接，并使用 READ COMMITTED 隔离级别开始一个事务，尝试读取表中的数据。  在这种情况下，代码无法读取数据，因为代码在第一个事务中无法通过在表上放置的锁进行读取，因而超时。  如果使用 REPEATABLE READ 和 SERIALIZABLE 隔离级别，因为这些隔离级别也无法通过第一个事务中放置的锁，因而会出现同样的结果。  
  
-   打开第四个连接，并使用 READ UNCOMMITTED 隔离级别开始一个事务，对 sqlTransaction1 中未提交的值执行脏读。  如果第一个事务未提交，数据库中永远不会真正存在此值。  
  
-   回滚第一个事务，并通过删除 **TestSnapshot** 表以及禁用 **AdventureWorks** 数据库的快照隔离来进行清理。  
  
> [!NOTE]
>  以下示例使用同一连接字符串，且其连接池已关闭。  如果某个连接被汇集，则重置其隔离级别并不会重置服务器的隔离级别。  因此，使用同一内部池连接的后续连接将会启动，且其隔离级别将设置为该池连接的隔离级别。  关闭连接池的另一种方法是为每个连接显式设置隔离级别。  
  
 [!code-csharp[DataWorks SnapshotIsolation.Demo#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.Demo/CS/source.cs#1)]
 [!code-vb[DataWorks SnapshotIsolation.Demo#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.Demo/VB/source.vb#1)]  
  
### 示例  
 以下示例演示修改数据时的快照隔离行为。  该代码执行下列操作：  
  
-   连接到 **AdventureWorks** 示例数据库并启用 SNAPSHOT 隔离。  
  
-   创建一个名为 **TestSnapshotUpdate** 的表并插入三行示例数据。  
  
-   使用 SNAPSHOT 隔离开始但是不完成 sqlTransaction1。  在事务中选择三行数据。  
  
-   创建第二个与 **AdventureWorks** 的 **SqlConnection**，并使用 READ COMMITTED 隔离级别创建第二个事务，更新在 sqlTransaction1 中选择的其中一行的值。  
  
-   提交 sqlTransaction2。  
  
-   返回 sqlTransaction1 并尝试更新 sqlTransaction1 已提交的相同的行。  将引发 3960 错误，sqlTransaction1 将自动回滚。  控制台窗口中将显示 **SqlException.Number** 和 **SqlException.Message**。  
  
-   执行清理代码以禁用 **AdventureWorks** 中的快照隔离并删除 **TestSnapshotUpdate** 表。  
  
 [!code-csharp[DataWorks SnapshotIsolation.DemoUpdate#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.DemoUpdate/CS/source.cs#1)]
 [!code-vb[DataWorks SnapshotIsolation.DemoUpdate#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.DemoUpdate/VB/source.vb#1)]  
  
### 对快照隔离使用锁提示  
 在前面的示例中，第一个事务选择数据，第二个事务在第一个事务完成前更新数据，在第一个事务尝试更新相同行时造成更新冲突。  通过在事务开始时提供锁提示，可以降低在需要很长时间的快照事务中发生更新冲突的机率。  以下 SELECT 语句使用 UPDLOCK 提示锁定所选行：  
  
```  
SELECT * FROM TestSnapshotUpdate WITH (UPDLOCK)   
  WHERE PriKey BETWEEN 1 AND 3  
```  
  
 使用 UPDLOCK 锁提示将阻止在第一个事务完成之前尝试更新行的任何行。  这样可以保证所选行以后在事务中进行更新时不会发生冲突。  请参见“SQL Server 联机图书”中的“锁定提示”。  
  
 如果应用程序中存在许多冲突，快照隔离也许不是最佳的选择。  只有在确实需要时，才应使用提示。  应用程序的设计不应使其操作始终依赖于锁提示。  
  
## 请参阅  
 [SQL Server 和 ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)