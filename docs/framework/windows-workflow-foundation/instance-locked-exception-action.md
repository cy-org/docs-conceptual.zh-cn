---
title: "实例锁定异常操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 164a5419-315c-4987-ad72-54cbdb88d402
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 实例锁定异常操作
利用 SQL 工作流实例存储的 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A> 属性，可以指定当 SQL 持久性提供程序收到 <xref:System.Runtime.DurableInstancing.InstanceLockedException> 时应采取什么操作。当持久性提供程序尝试锁定当前已由另一个服务主机锁定的工作流服务实例时，将收到此异常。此属性的值有 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>、<xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction> 和 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>。默认值为 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>。以下列表对这三个选项进行了说明：  
  
-   <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>.服务主机不会尝试锁定工作流服务实例，并将 <xref:System.Runtime.DurableInstancing.InstanceLockedException> 传递给调用方。如果您的工作流停留在内存的时间超过 60 秒，则请使用 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction> 作为重试。   默认值为 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>。  
  
-   <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>.服务主机将使用线性间隔重试间隔重新尝试锁定工作流服务实例，并在序列结尾将 <xref:System.Runtime.DurableInstancing.InstanceLockedException> 传递给调用方。如果工作流将停留在内存约之间 5\-60 秒，并且邮件分批到达哪里更有可能的消息发送到进程的同一主机上的同一实例的所有邮件之前卸载工作流中，使用 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>，不浪费资源的情况下达到最佳的延迟。  
  
-   <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>.服务主机将使用重试间的指数备值间隔重新尝试锁定工作流服务实例，并在序列结尾将异常传递给调用方。如果您的工作流在内存中停留的时间很短（少于 5 秒）或网站网页农场很大并且另一个消息传递到同一主机的机会不是很高，请使用 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction> 实现最佳的延迟。  
  
 实例锁定异常操作功能支持以下方案。在所有方案中，如果将 SqlWorkflowInstanceStore 的 instanceLockedExceptionAction 属性设置为 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction> 或 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>，主机会定期透明地重试获取对实例的锁定。  
  
1.  **支持正常关机和应用程序域的重叠回收。**假定正在回收某一服务主机正在运行工作流服务实例的 **AppDomain**，并且当正常关闭旧 **AppDomain** 时，将启动新 **AppDomain** 以便并行处理新请求。此关闭将等待一段时间，直到工作流服务实例空闲为止，然后将保存并卸载这些实例。新 **AppDomain** 中的任何主机尝试锁定其中的某个实例都会导致 <xref:System.Runtime.DurableInstancing.InstanceLockedException>。  
  
2.  **在同类服务器场中水平扩展持久性工作流。**假定服务器场中正在运行工作流实例的某一节点崩溃，并且工作流主机无法移除对其正在运行的实例的锁定。当场中的另一节点上运行的服务主机接收到有关该工作流实例的消息时，它会尝试获取对这些实例的锁定，并且将接收到 <xref:System.Runtime.DurableInstancing.InstanceLockedException>。该锁定将在一段时间后过期，这是因为原本应续订锁定的主机已不再存在。  
  
     **在同类服务器场中水平扩展持久性工作流。**假定您希望使用支持 NLB（网络负载平衡器）的多个主机水平扩展持续性工作流，在场中的一个节点上运行的工作流主机加载了一个工作流实例，并且正在处理一条消息，该实例的下一条消息将路由到在另一节点上运行的主机，其原因在于 NLB 没有相应的路由算法将多条消息传递到已在运行该实例的主机。接收到此消息后，第二个主机尝试加载工作流实例，并接收到 <xref:System.Runtime.DurableInstancing.InstanceLockedException>，这是因为第一个主机已锁定该实例。第一个主机在处理完第一条消息后，将解除对该实例的锁定，第二个主机将在下次重试时获取锁定，然后加载该实例，并处理第二条消息。