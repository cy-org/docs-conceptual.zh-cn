---
title: "工作流持久性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "编程 [WF], 持久性"
ms.assetid: 39e69d1f-b771-4c16-9e18-696fa43b65b2
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# 工作流持久性
工作流持久性是指独立于进程或计算机信息持续捕获工作流实例的状态。其目的在于：在发生系统故障时为工作流实例提供一个已知恢复点，通过卸载当前未主动执行工作的工作流实例来节省内存，或者将工作流实例状态从服务器场中的一个节点移至另一个节点。  
  
 持久性支持进程灵活性、可扩展性、故障恢复以及更有效地管理内存的功能。持久性进程包括标识持久点、收集要保存的数据以及将数据实际存储最终委托给持久性提供程序。  
  
 若要对工作流启用持久性，您需要将实例存储与 **WorkflowApplication** 或 **WorkflowServiceHost** 相关联，如[如何：对工作流和工作流服务启用持久性](../../../docs/framework/windows-workflow-foundation//how-to-enable-persistence-for-workflows-and-workflow-services.md)中所述。**WorkflowApplication** 和 **WorkflowServiceHost** 使用与其关联的实例存储将工作流实例保存到持久性存储中，并根据持久性存储中存储的工作流实例数据将工作流实例加载到内存中。  
  
 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]附带的 **SqlWorkflowInstanceStore** 类允许在 SQL Server 2005 或 SQL Server 2008 数据库中保存有关工作流实例的数据和元数据。有关更多详细信息，请参见 [SQL 工作流实例存储](../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)。  
  
 若要存储和加载应用程序特定数据以及与工作流实例相关的信息，您可以创建用于扩展 <xref:System.Activities.Persistence.PersistenceParticipant> 类的持久性参与者。持久性参与者参与持久性进程的目的是：将可序列化的自定义数据保存到持久性存储中，将实例存储中的数据加载到内存中，以及在持久性事务下执行任何其他逻辑。有关更多信息，请参见 [持久性参与者](../../../docs/framework/windows-workflow-foundation//persistence-participants.md)。  
  
 Windows Server App Fabric 大大简化了配置持久性的进程。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Windows Server App Fabric 的持久性理念](http://go.microsoft.com/fwlink/?LinkId=201200)  
  
## 隐式持久点  
 以下列表包含当实例存储与工作流关联时持久化工作流所依据的条件的示例。  
  
-   当 **TransactionScope** 活动完成时或 **TransactedReceiveScope** 活动完成时。  
  
-   当工作流实例变为空闲状态，且对工作流主机设置了 **WorkflowIdleBehavior** 时。例如，当使用消息传递活动或 **Delay** 活动时会发生此情况。  
  
-   当 WorkflowApplication 变为空闲状态且将应用程序的 **PersistableIdle** 属性设置为 **PersistableIdleAction.Persist** 时。  
  
-   当指示主机应用程序持久化或卸载工作流实例时。  
  
-   当终止工作流实例或工作流实例结束时。  
  
-   当执行 **Persist** 活动时。  
  
-   当使用 Windows Workflow Foundation 的早期版本开发的工作流实例在可互操作执行过程中遇到持久点时。  
  
## 本节内容  
  
-   [SQL 工作流实例存储](../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)  
  
-   [实例存储区](../../../docs/framework/windows-workflow-foundation//instance-stores.md)  
  
-   [持久性参与者](../../../docs/framework/windows-workflow-foundation//persistence-participants.md)  
  
-   [持久性最佳做法](../../../docs/framework/windows-workflow-foundation//persistence-best-practices.md)  
  
-   [非持久工作流实例](../../../docs/framework/windows-workflow-foundation//non-persisted-workflow-instances.md)  
  
-   [暂停和继续工作流](../../../docs/framework/windows-workflow-foundation//pausing-and-resuming-a-workflow.md)