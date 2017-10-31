---
title: "OLE DB、ODBC 和 Oracle 连接池 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2bd83b1e-3ea9-43c4-bade-d9cdb9bbbb04
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# OLE DB、ODBC 和 Oracle 连接池
池连接可以显著提高应用程序的性能和可缩放性。  本节介绍用于 OLE DB、ODBC 和 Oracle 的 .NET Framework 数据提供程序的连接池。  
  
## OleDb 连接池  
 OLE DB .NET Framework 数据提供程序使用 OLE DB 会话池自动管理连接池。  连接字符串参数可用于启用或禁用包括池在内的 OLE DB 服务。  例如，以下连接字符串禁用 OLE DB 会话池和自动事务登记。  
  
```  
Provider=SQLOLEDB;OLE DB Services=-4;Data Source=localhost;Integrated Security=SSPI;  
```  
  
 我们建议您在使用完连接后始终将其关闭或释放，以便连接可以返回到池。  不是显式关闭的连接可能无法返回池。  例如，如果连接已超出范围但没有显式关闭，则仅当达到最大池大小而该连接仍然有效时，该连接才会返回到连接池中。  
  
 有关 OLE DB 会话池或资源池以及如何通过重写 OLE DB 提供程序服务默认值禁用池的更多信息，请参见 MSDN Library 中的 [OLE DB 程序员指南](http://go.microsoft.com/fwlink/?linkid=45232)（可能为英文网页）。  
  
## Odbc 连接池  
 ODBC .NET Framework 数据提供程序的连接池由用于该连接的 ODBC 驱动程序管理器管理，不受 ODBC .NET Framework 数据提供程序的影响。  
  
 要启用或禁用连接池，在“控制面板”的“管理工具”文件夹中打开“ODBC 数据源管理器”。  通过“连接池”选项卡可以为每个已安装的 ODBC 驱动程序指定连接池参数。  请注意，对特定 ODBC 驱动程序所做的更改会影响所有使用该 ODBC 驱动程序的应用程序。  
  
 有关 ODBC 连接池的更多信息，请参见 MSDN Library 中的[信息：有关 ODBC 连接池的常见问题](http://support.microsoft.com/kb/169470)（可能为英文网页）。  
  
## OracleClient 连接池  
 Oracle .NET Framework 数据提供程序自动为 ADO.NET 客户端应用程序提供连接池。  您也可以提供几个连接字符串修饰符，用于控制连接池的行为（请参见本主题后文的“使用连接字符串关键字控制连接池”）。  
  
### 池的创建和分配  
 当连接打开时，将根据一种精确的匹配算法来创建连接池，该算法会使连接池与连接中的字符串相关联。  每个连接池都与一个不同的连接字符串相关联。  打开新连接时，如果连接字符串并非与现有池完全匹配，将创建一个新池。  
  
 连接池一旦创建，直到活动进程终止时才会被毁坏。  维护不活动的池或空池占用的系统资源非常少。  
  
### 连接的添加  
 连接池是为每个唯一的连接字符串创建的。  当创建一个池后，将创建多个连接对象并将其添加到该池中，以满足最小池大小的要求。  连接将根据需要添加到池中，直至达到最大池大小。  
  
 在请求 <xref:System.Data.OracleClient.OracleConnection> 对象时，如果存在可用的连接，则将从池中获取该对象。  要成为可用连接，该连接当前必须未被使用，具有匹配的事务上下文或者不与任何事务上下文相关联，并且具有与服务器的有效链接。  
  
 如果已达到最大池大小且不存在可用的连接，则该请求将会排队。  当连接被释放回池中时，连接池管理程序通过重新分配连接来满足这些请求。  连接在关闭或断开时释放回池中。  
  
### 连接的移除  
 如果连接长时间空闲，或池进程检测到与服务器的连接已断开，连接池进程会将该连接从池中移除。  请注意，只有在尝试与服务器进行通信后，才可以检测到这种情况。  如果发现某连接不再连接到服务器，则会将其标记为无效。  连接池管理程序会定期扫描连接池，查找已释放到池中并标记为无效的对象。  找到后，这些连接将被永久移除。  
  
 如果存在一个与已消失的服务器的连接，如果连接池进程尚未检测到断开的连接并将连接标记为无效，可以从池中提取此连接。  当发生这种情况时，将生成异常。  但是，为了将该连接释放回池中，仍必须将其关闭。  
  
 不要在类的 `Finalize` 方法中对 `Connection`、`DataReader` 或任何其他托管对象调用 `Close` 或 `Dispose`。  在终结器中，仅释放类直接拥有的非托管资源。  如果类不拥有任何非托管资源，则不要在类定义中包含 `Finalize` 方法。  有关详细信息，请参阅[Garbage Collection](../../../../docs/standard/garbage-collection/index.md)。  
  
### 事务支持  
 连接是根据事务上下文来从池中取出并进行分配的。  请求线程和所分配的连接的上下文必须匹配。  因此，每个连接池实际上又分为不具有关联事务上下文的连接以及 *N* 个各自包含与一个特定事务上下文的连接的子部分。  
  
 当连接关闭时，它将被释放回池中，并根据其事务上下文放入相应的子部分。  因此，即使分布式事务仍然挂起，仍可以关闭该连接而不会生成错误。  这样，您就可以在随后提交或中止分布式事务。  
  
### 使用连接字符串关键字控制连接池  
 <xref:System.Data.OracleClient.OracleConnection> 对象的 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> 属性支持连接字符串键\/值对，可以用于调整连接池逻辑的行为。  
  
 下表描述了可用于调整连接池行为的 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> 值。  
  
|名称|默认|描述|  
|--------|--------|--------|  
|`Connection Lifetime`|0|连接返回到池中后，创建时间将与当前时间进行比较，如果时间跨度（秒）超过 `Connection Lifetime` 指定的值，该连接将被破坏。  在聚集配置中可以使用它来强制在运行服务器和刚联机的服务器之间达到负载平衡。<br /><br /> 如果值为零 \(0\)，则将使池连接具有最大的超时期限。|  
|`Enlist`|'true'|当为 `true` 时，如果存在事务上下文，池管理程序将自动在创建线程的当前事务上下文中登记连接。|  
|`Max Pool Size`|100|池中允许的最大连接数。|  
|`Min Pool Size`|0|池中维护的最小连接数。|  
|`Pooling`|'true'|当为 `true` 时，将从相应的池中取出连接，或者在必要时创建连接并将其添加到相应的池中。|  
  
## 请参阅  
 [连接池](../../../../docs/framework/data/adonet/connection-pooling.md)   
 [性能计数器](../../../../docs/framework/data/adonet/performance-counters.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)