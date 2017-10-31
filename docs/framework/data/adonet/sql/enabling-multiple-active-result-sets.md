---
title: "启用多个活动结果集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 启用多个活动结果集
多个活动结果集 \(MARS\) 是一项用于 SQL Server 的功能，可用来对单个连接执行多个批处理。  如果对 SQL Server 启用了 MARS，使用的每个命令对象将向该连接添加一个会话。  
  
> [!NOTE]
>  一个 MARS 会话打开一个逻辑连接以供 MARS 使用，然后为每个活动命令打开一个逻辑连接。  
  
## 在连接字符串中启用和禁用 MARS  
  
> [!NOTE]
>  下列连接字符串使用随 SQL Server 提供的 **AdventureWorks** 示例数据库。  提供的连接字符串假定数据库安装在名为 MSSQL1 的服务器上。  根据环境的需要修改连接字符串。  
  
 默认情况下禁用 MARS 功能。  可以通过在连接字符串中添加“MultipleActiveResultSets\=True”关键字对来启用此功能。"  True”是启用 MARS 的唯一有效值。  以下示例演示如何连接到 SQL Server 实例以及如何指定应启用 MARS。  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=True"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
 可以通过在连接字符串中添加“MultipleActiveResultSets\=False”关键字对来禁用此功能。"  False”是禁用 MARS 的唯一有效值。  以下连接字符串演示如何禁用 MARS。  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=False"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## 使用 MARS 时的特殊注意事项  
 通常情况下，现有的应用程序不需要修改，即可使用启用 MARS 的连接。  但是，如果要在应用程序中使用 MARS 功能，应了解下列特殊注意事项。  
  
### 语句交替  
 MARS 操作在服务器上同步执行。  允许 SELECT 和 BULK INSERT 语句的语句交替。  但是，数据操作语言 \(DML\) 和数据定义语言 \(DDL\) 语句会自动执行。  将阻止任何在执行原子批处理时尝试执行的语句。  服务器上的并行执行不是 MARS 功能。  
  
 如果在 MARS 连接下提交两个批处理，其中一个批处理包含 SELECT 语句，另一个包含 DML 语句，DML 可以在 SELECT 语句执行过程中开始执行。  但是，DML 语句必须运行完成，SELECT 语句才可以继续执行。  如果两个语句在相同事务下运行，读取操作将看不到 DML 语句在 SELECT 语句开始执行后所作的任何更改。  
  
 SELECT 语句中的 WAITFOR 语句在等待时不生成事务，即直到生成第一行时才生成事务。  这意味着在 WAITFOR 语句等待时，无法在相同连接内执行任何其他批处理。  
  
### MARS 会话缓存  
 如果打开启用了 MARS 的连接，将创建一个逻辑会话，这样会增加系统开销。  为了使系统开销最小并提高性能，**SqlClient** 将 MARS 会话缓存在连接内。  缓存最多可以包含 10 个 MARS 会话。  用户不可调整此值。  如果达到会话限制，将创建一个新会话 — 不会生成错误。  缓存及其包含的会话针对特定连接；不在连接之间共享。  会话释放后，除非已达到池的上限，否则，将返回池中。  如果缓存池已满，会话将关闭。  MARS 会话不会过期。  只在连接对象断开后才进行清理。  MARS 会话缓存不会预加载。  如果应用程序需要更多的会话，将加载该会话。  
  
### 线程安全  
 MARS 操作不是线程安全的。  
  
### 连接池  
 启用 MARS 的连接像任何其他连接一样建立池连接。  如果应用程序打开两个连接，一个启用了 MARS，一个禁用了 MARS，这两个连接将位于独立的池中。  有关详细信息，请参阅[SQL Server 连接池 \(ADO.NET\)](../../../../../docs/framework/data/adonet/sql-server-connection-pooling.md)。  
  
### SQL Server 批处理执行环境  
 打开连接时，将定义默认的环境。  然后，将此环境复制到逻辑 MARS 会话中。  
  
 批处理执行环境包括下列组件：  
  
-   设置选项（例如 ANSI\_NULLS、DATE\_FORMAT、LANGUAGE、TEXTSIZE）  
  
-   安全上下文（用户\/应用程序角色）  
  
-   数据库上下文（当前数据库）  
  
-   执行状态变量（例如 @@ERROR、@@ROWCOUNT、@@FETCH\_STATUS @@IDENTITY）  
  
-   顶级临时表  
  
 使用 MARS，默认的执行环境将与连接关联。  在给定连接下开始执行的每个新的批处理会接收默认环境的副本。  只要代码在给定的批处理下执行，对环境所作的所有更改将作用于特定的批处理。  执行完成后，执行设置将复制到默认环境中。  如果单个批处理发出的多个命令要在相同事务下顺序执行，语义与通过与早期客户端或服务器有关的连接公开的语义相同。  
  
### 并行执行  
 使用 MARS 后，并非不再需要在应用程序中使用多个连接。  如果应用程序需要对服务器真正地并行执行命令，应使用多个连接。  
  
 例如，考虑以下方案。  创建了两个命令对象，一个用于处理结果集，另一个用于更新数据；这两个命令对象通过 MARS 共享公共连接。  在此方案中，`Transaction`.`Commit` 在更新时失败，直到在第一个命令对象上读取了所有结果，并生成以下异常：  
  
 消息：其他会话正在使用事务的上下文。  
  
 源：.Net SqlClient 数据提供程序  
  
 要求：\(null\)  
  
 收到：System.Data.SqlClient.SqlException  
  
 可以通过三种方式处理此方案：  
  
1.  在创建读取器之后开始事务，使读取器不是事务的一部分。  每次更新将变为读取器自己的事务。  
  
2.  在读取器关闭之后提交所有工作。  对于大量的更新批处理，可能会这样做。  
  
3.  不使用 MARS；而是对每个命令对象使用独立的连接，就像在 MARS 之前一样。  
  
### 检测 MARS 支持  
 应用程序可以通过读取 `SqlConnection.ServerVersion` 值来检查 MARS 支持。   SQL Server 2005 的主版本号应为 9，SQL Server 2008 的主版本号应为 10。  
  
## 请参阅  
 [多活动结果集 \(MARS\)](../../../../../docs/framework/data/adonet/sql/multiple-active-result-sets-mars.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)