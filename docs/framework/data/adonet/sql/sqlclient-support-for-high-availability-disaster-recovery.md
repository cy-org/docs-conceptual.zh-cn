---
title: "SqlClient 对高可用性的支持，灾难恢复 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 61e0b396-09d7-4e13-9711-7dcbcbd103a0
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# SqlClient 对高可用性的支持，灾难恢复
本主题介绍对高可用性、灾难恢复（AlwaysOn 可用性组）的 SqlClient支持（[!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)] 中的新功能）。  AlwaysOn 可用性组功能已添加到 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 中。  有关 AlwaysOn 可用性组的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 联机丛书。  
  
 现在，您可以在连接属性中指定一个 具有（高可用性、灾难恢复功能）的可用性组 \(AG\) 的可用性组侦听器或 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 故障转移群集实例。  如果 SqlClient 应用程序连接到发生故障转移的 AlwaysOn 数据库，原始连接会中断，而且应用程序必须打开一个新连接以在故障转移之后继续工作。  
  
 如果您没有连接到可用性组侦听器或 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 故障转移群集实例，并且如果多个 IP 地址关联一个主机名，SqlClient 将按顺序循环访问与 DNS 条目关联的所有 IP 地址。  如果 DNS 服务器返回的第一个 IP 地址未绑定到到任何网络接口卡 \(NIC\)，这可能非常耗时。  连接到一个可用性组侦听器或 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 故障转移群集实例时，SqlClient 尝试并行建立所有 IP 地址的连接，如果一个连接尝试成功，驱动程序将丢弃所有挂起的连接尝试。  
  
> [!NOTE]
>  增加连接超时值和实现连接重试逻辑会增加应用程序连接到可用性组的概率。  此外，由于故障转移，连接可能失败，所以您应当实现连接重试逻辑，重试失败的连接，直到它重新连接。  
  
 以下连接属性已添加到 [!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)] 中的 SqlClient：  
  
-   `ApplicationIntent`  
  
-   `MultiSubnetFailover`  
  
 您可通过编程方式修改这些连接字符串关键字：  
  
1.  <xref:System.Data.SqlClient.SqlConnectionStringBuilder.ApplicationIntent%2A>  
  
2.  <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A>  
  
## 使用 MultiSubnetFailover 连接  
 连接到 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 可用性组侦听器或 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 故障转移群集实例时， 始终指定 `MultiSubnetFailover=True`。  对于单子网和多子网 AlwaysOn 拓扑，`MultiSubnetFailover` 可使 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 中的所有可用性组或故障转移群集实例故障转移速度变快，大大缩短故障转移时间。  在多子网故障转移期间，客户端将尝试并行连接。  在子网故障转移期间，将积极重试 TCP 连接。  
  
 `MultiSubnetFailover` 连接属性指示应用程序将部署到可用性组或 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 故障转移群集实例，并且 SqlClient 将通过连接到所有的 IP 地址尝试连接到主 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 实例上的数据库。  为连接指定 `MultiSubnetFailover=True` 时，客户端尝试 TCP 连接的频率比操作系统的默认 TCP 重新传输间隔快。  这使得在 AlwaysOn 可用性组或 AlwaysOn 故障转移群集实例进行故障转移后更快地重新连接，它同时适用于单子网\/多子网可用性组和故障转移群集实例。  
  
 有关 SqlClient 中的连接字符串关键字的更多信息，请参见 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>。  
  
 如果在连接到除可用性组侦听器或 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 故障转移群集实例之外的对象时指定 `MultiSubnetFailover=True`，可能导致性能下降，因此不支持这样做。  
  
 遵循下列准则连接到可用性组或 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012 故障转移群集实例中的服务器：  
  
-   连接到单子网或多子网时使用 `MultiSubnetFailover` 连接属性，这样可提高它们的性能。  
  
-   要连接到可用性组，请在连接字符串中指定作为服务器的可用性组的可用性组侦听器。  
  
-   连接到一个配置超过 64 个 IP 地址的 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 实例会导致连接失败。  
  
-   根据身份验证类型（[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 身份验证、 Kerberos 身份验证或 Windows 身份验证），使用 `MultiSubnetFailover` 连接属性的应用程序行为可能不受影响。  
  
-   增加 `Connect Timeout` 的值以延长故障转移时间并减少应用程序连接重试次数。  
  
-   不支持分布式事务。  
  
 如果只读路由无效，在下列情况下连接到辅助副本位置将失败：  
  
1.  如果未配置辅助副本位置以接受连接。  
  
2.  如果应用程序使用 `ApplicationIntent=ReadWrite`（将在下文讨论），并且辅助副本位置配置为只读访问。  
  
 在只读辅助副本上不支持 <xref:System.Data.SqlClient.SqlDependency>。  
  
 如果主副本配置为拒绝只读工作负荷并且连接字符串包含 `ApplicationIntent=ReadOnly`，连接将失败。  
  
## 从数据库镜像升级到使用多子网群集  
 如果 `MultiSubnetFailover` 和 `Failover Partner` 连接关键字在连接字符串中存在，或者使用 `MultiSubnetFailover=True` 和 TCP 以外的其他协议，则会出现连接错误 \(<xref:System.ArgumentException>\)。  如果使用 `MultiSubnetFailover`且 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 返回一个故障转移伙伴响应指示它是数据库镜像对的一部分，也会出现错误 \(<xref:System.Data.SqlClient.SqlException>\) 。  
  
 如果您将当前使用数据库镜像的 SqlClient 应用程序升级到多子网方案，应删除 `Failover Partner` 连接属性并使用 `MultiSubnetFailover` 设置为 `True` 的属性替换它，同时使用可用性组侦听器替换连接字符串中的服务器名称。  如果连接字符串使用 `Failover Partner` 和 `MultiSubnetFailover=True`，驱动程序将生成错误。  但是，如果连接字符串使用 `Failover Partner` 和 `MultiSubnetFailover=False`（或 `ApplicationIntent=ReadWrite`），应用程序将使用数据库镜像。  
  
 如果在 AG 的主数据库上使用数据库镜像，并且如果 `MultiSubnetFailover=True` 被用于连接到主数据库而非可用性组侦听器的连接字符串中，驱动程序将返回错误。  
  
## 指定应用程序意向  
 当 `ApplicationIntent=ReadOnly` 时，客户端在连接到启用 AlwaysOn 的数据库时请求读工作负荷。  服务器将在连接时和 USE 数据库语句期间执行该意向，但是仅针对启用 Always On 的数据库。  
  
 `ApplicationIntent` 关键字不适用于旧的只读数据库。  
  
 数据库可以允许或不允许针对的 AlwaysOn 数据库上的读工作负荷。  （使用 `PRIMARY_ROLE` 和 `SECONDARY_ROLE` [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] 语句的 `ALLOW_CONNECTIONS` 子句可做到这点。）  
  
 `ApplicationIntent` 关键字用于启用只读路由。  
  
## 只读路由  
 只读路由是一种可以确保数据库只读副本的可用性的功能。  要启用只读路由：  
  
1.  您必须连接到 Always On 可用性组的可用性组侦听器。  
  
2.  `ApplicationIntent` 连接字符串关键字必须设置为 `ReadOnly`。  
  
3.  可用性组必须由数据库管理员配置以启用只读路由。  
  
 使用只读路由的多个连接并非连接到相同的只读副本。  数据库同步的更改或服务器路由配置的更改可能导致客户端连接到不同的只读副本。  为确保所有只读请求连接到相同的只读副本，请不要将可用性组侦听器传递给 `Data Source` 连接字符串关键字。   请指定只读实例的名称。  
  
 只读路由可能需要比连接到主副本更长的时间，因为只读路由要先连接到主副本，然后查找最可能可用的可读辅助副本。  为此，您应增加您的登录超时值。  
  
## 请参阅  
 [SQL Server 功能和 ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-features-and-adonet.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)