---
title: "CustomPeerResolverService 内部：客户端注册 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 40236953-a916-4236-84a6-928859e1331a
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# CustomPeerResolverService 内部：客户端注册
网格中的每个节点都通过 `Register` 函数，将自己的终结点信息发布到解析程序服务。  解析程序服务将此信息存储为注册记录。  此记录包含节点的唯一标识符 \(RegistrationID\) 和终结点信息 \(PeerNodeAddress\)。  
  
## 过时记录和过期时间  
 理想情况下，当节点离开网格时，它将调用 `Unregister` 函数，让解析程序服务删除相关注册项。  有时，节点会在调用 `Unregister` 之前关闭或无法访问，从而留下过时的注册记录。  
  
 解析程序服务中的过时记录可能导致连接失败。  如果尝试连接到网格的节点从解析程序服务收到过时的连接信息，则需要更长的时间才能成功加入网格。  过时记录还会占用内存。  如果没有有效的清除过程，用于存储注册的缓存最终可能会溢出，并使解析程序服务崩溃。  
  
 <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> 用过期时间 \(DateTime\) 标记每条记录，并将该信息存储在记录中。  服务使用过期时间来标识过时的记录。  自定义实现应执行类似的操作。  
  
## RefreshInterval 和 CleanupInterval  
 `RefreshInterval` 的<xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> 属性定义了注册记录在服务的注册查找表中保持有效的持续时间。  对于给定的记录，在为此属性提供的时间到期后，该记录将过时，并标记为待删除。  
  
 `CleanupInterval` 的 <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> 属性通知服务搜索和删除过时注册记录的频率。  `CleanupInterval` 应设置为大于或等于对服务设置的 `RefreshInterval` 时间。  
  
 若要实现您自己的解析程序服务，需编写一个维护函数来删除过时的注册记录。  有若干方法可实现此操作：  
  
-   **定期维护**：将计时器设置为定期关闭，并遍历数据存储区以删除旧记录。  <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> 使用此方法。  
  
-   **被动删除**：在服务已转为执行其他功能时，标识和删除过时的记录，而不是按固定的时间间隔主动搜索过时的记录。  这可能会延长对解析程序客户端请求的响应时间，但此方法不需要计时器。此外，如果预期很少有节点会不调用 `Unregister` 便离开，此方法将更有效。  
  
## RegistrationLifetime 和 Refresh  
 节点向解析程序服务注册时，它将从该服务收到一个 <xref:System.ServiceModel.PeerResolvers.RegisterResponseInfo> 对象。  此对象具有 `RegistrationLifetime` 属性，该属性告知节点，注册将在多久之后过期并被解析程序服务删除。  例如，如果 `RegistrationLifetime` 为 2 分钟，则节点需要在 2 分钟内调用 `Refresh`，以确保记录保持不过时状态，以免被删除。  解析程序服务收到 `Refresh` 请求时，它会查找记录并重置过期时间。  Refresh 返回一个具有 <xref:System.ServiceModel.PeerResolvers.RefreshResponseInfo> 属性的 `RegistrationLifetime` 对象。  
  
## 请参阅  
 [对等解析程序](../../../../docs/framework/wcf/feature-details/peer-resolvers.md)