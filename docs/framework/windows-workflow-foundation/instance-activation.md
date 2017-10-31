---
title: "实例激活 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 134c3f70-5d4e-46d0-9d49-469a6643edd8
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 实例激活
SQL 工作流实例存储运行一个内部任务，该任务将定期唤醒并检测持久性数据库中是否有可运行或可激活的工作流实例。如果找到可运行的工作流实例，SQL 工作流实例存储将通知能够激活该实例的工作流主机。如果实例存储找到可激活的工作流实例，它将通知用于激活工作流主机的泛型主机，而泛型主机将运行此工作流实例。本主题的以下各节详细说明了实例激活过程。  
  
##  <a name="RunnableSection"></a> 检测和激活可运行的工作流实例  
 如果某个工作流实例未处于挂起状态或完成状态并且满足以下条件，SQL 工作流实例存储则将该工作流实例视为“可运行”：  
  
-   实例处于解除锁定状态，并且具有已过期的挂起计时器。  
  
-   实例上的锁定已过期。  
  
-   实例处于解除锁定状态，并且其状态为“正在执行”。  
  
 当 SQL 工作流实例存储找到可运行的实例时，将引发 <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent>。此后，SqlWorkflowInstanceStore 将停止监视，直到在该存储上调用一次 <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand>。  
  
 已订阅 <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent> 且能够加载该实例的工作流主机将针对实例存储执行 <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand>，以将该实例加载到内存中。如果工作流主机和工作流实例将元数据属性 **WorkflowServiceType** 设置为相同值，则认为该主机能够加载该实例。  
  
## 检测和激活可激活的工作流实例  
 如果工作流实例可运行，并且计算机上未运行有能够加载该实例的工作流主机，则将该实例视为“可激活”。有关可运行的工作流实例的定义，请参见上面的“检测和激活可运行的工作流实例”。  
  
 当 SQL 工作流实例存储在数据库中找到可激活的工作流实例时，将引发 <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent>。此后，SqlWorkflowInstanceStore 将停止监视，直到在该存储上调用一次 <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand>。  
  
 当已订阅 <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent> 的泛型主机接收到此事件时，它将针对实例存储执行 <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand> 以获取创建工作流主机所需的激活参数。泛型主机使用这些激活参数来创建工作流主机，后者又依次加载并运行可运行的服务实例。  
  
## 泛型主机  
 泛型主机是指这样的主机：将泛型主机的元数据属性 **WorkflowServiceType** 的值设置为 **WorkflowServiceType.Any**，以指示该主机可以处理任何工作流类型。泛型主机采用名为 **ActivationType** 的 XName 参数。  
  
 目前，SQL 工作流实例存储支持 ActivationType 参数值设置为 **WAS** 的泛型主机。如果未将 ActivationType 设置为 WAS，SQL 工作流实例存储将引发 <xref:System.Runtime.DurableInstancing.InstancePersistenceException>。附带了 [!INCLUDE[dublin](../../../includes/dublin-md.md)] 的工作流管理服务是将激活类型设置为 **WAS** 的泛型主机。  
  
 为了实现 WAS 激活，泛型主机需要一组激活参数来派生激活新主机所在的终结点地址。用于 WAS 激活的激活参数包括：站点名称、应用程序路径（相对于站点）和服务路径（相对于应用程序）。SQL 工作流实例存储在执行 <xref:System.Activities.DurableInstancing.SaveWorkflowCommand> 期间存储这些激活参数。  
  
## 可运行实例的检测周期  
 SQL 工作流实例存储的“可运行实例的检测周期”属性指定一个时间段，在该时间段后，SQL 工作流实例存储将运行一个检测任务，来检测在上一检测周期之后持久性数据库中是否有任何可运行或可激活的工作流实例。有关此属性的更多详细信息，请参见[可运行实例的检测周期](../../../docs/framework/windows-workflow-foundation//runnable-instances-detection-period.md)。