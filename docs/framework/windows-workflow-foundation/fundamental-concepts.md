---
title: "Windows 工作流基础概念 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e930e80-5060-45d2-8a7a-95c0690105d4
caps.latest.revision: 27
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 27
---
# Windows 工作流基础概念
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 中的工作流开发会运用一些开发人员可能还不熟悉的概念。本主题介绍其中的一些概念以及如何实现这些概念。  
  
## 工作流和活动  
 工作流是构成进程模型的操作的结构化集合。工作流中的每个操作都建模为一个活动。主机将 <xref:System.Activities.WorkflowInvoker> 用于调用工作流（就好像是一个方法），将 <xref:System.Activities.WorkflowApplication> 用于对单个工作流实例的执行进行显式控制，并将 <xref:System.ServiceModel.WorkflowServiceHost> 用于在多实例方案中进行基于消息的交互，从而实现与工作流的交互。由于工作流的步骤定义为活动的层次结构，因此层级中最顶端的活动可以认为是定义工作流本身。此层次结构模型替代以前版本中的显式 `SequentialWorkflow` 和 `StateMachineWorkflow` 类。活动自身可作为其他活动的集合（使用 <xref:System.Activities.Activity> 类作为基础，通常使用 XAML 定义）开发；或者使用 <xref:System.Activities.CodeActivity> 或 <xref:System.Activities.NativeActivity> 类进行自定义创建，前者可以使用运行时进行数据访问，而后者则向活动作者公开工作流运行时范围。使用 <xref:System.Activities.CodeActivity> 和 <xref:System.Activities.NativeActivity> 类开发的活动是使用符合 CLR 的语言创建的，如 C\#。  
  
## 活动数据模型  
 活动使用下表中所示的类型存储和共享数据。  
  
|||  
|-|-|  
|变量|存储活动中的数据。|  
|参数|将数据移入和移出活动。|  
|表达式|带有在参数绑定中使用的提升的返回值的活动。|  
  
## 工作流运行时  
 工作流运行时是工作流进行执行的环境。 <xref:System.Activities.WorkflowInvoker> 这是执行工作流的最简单的方法。宿主为以下操作使用 <xref:System.Activities.WorkflowInvoker>：  
  
-   以同步方式调用工作流。  
  
-   向工作流提供输入或从其中检索输出。  
  
-   添加供活动使用的扩展。  
  
 <xref:System.Activities.ActivityInstance> 是线程安全的代理，宿主可以使用该代理与运行时进行交互。宿主为以下操作使用 <xref:System.Activities.ActivityInstance>：  
  
-   通过创建实例或从实例存储区中加载实例的方法来获取实例。  
  
-   接收实例生命周期事件通知。  
  
-   控制工作流执行。  
  
-   向工作流提供输入或从其中检索输出。  
  
-   向工作流发出继续信号并将值传递到工作流中。  
  
-   保存工作流数据。  
  
-   添加供活动使用的扩展。  
  
 活动通过使用相应的 <xref:System.Activities.ActivityContext> 派生类获得访问工作流运行时环境的权限，例如 <xref:System.Activities.NativeActivityContext> 或 <xref:System.Activities.CodeActivityContext>。这些元素使用此类来解析参数和变量，以便安排子活动和实现多种其他用途。  
  
## 服务  
 工作流提供一种使用消息活动实现和访问松耦合服务的自然方法。消息活动建立在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 是，并且是用于将数据获取到工作流外的主要机制。您可将消息活动组合在一起，以对任何你希望的消息交换模式进行建模。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] 请参见 [消息传递活动](../../../docs/framework/wcf/feature-details/messaging-activities.md)。使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 类承载工作流服务。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][承载工作流服务概述](../../../docs/framework/wcf/feature-details/hosting-workflow-services-overview.md).[!INCLUDE[crabout](../../../includes/crabout-md.md)] 工作流服务，请参见[工作流服务](../../../docs/framework/wcf/feature-details/workflow-services.md)  
  
## 持久性、卸载和长时间运行的工作流  
 Windows 工作流通过提供以下功能，简化了创作长时间运行的反应式程序的过程：  
  
-   访问外部输入的活动。  
  
-   能够创建可由宿主侦听程序恢复的 <xref:System.Activities.Bookmark> 对象。  
  
-   能够保存工作流数据并卸载工作流，然后作为对特定工作流中恢复 <xref:System.Activities.Bookmark> 对象的响应，重新加载和重新激活工作流。  
  
 工作流会持续地执行活动，直到没有任何要执行的活动或者所有当前正在执行的活动均在等待输入为止。在后一种情况下，工作流处于空闲状态。通常宿主会卸载进入空闲状态的工作流，并在收到消息时将其重载到继续执行。<xref:System.ServiceModel.Activities.WorkflowServiceHost> 为此功能提供功能，并提供了可扩展的卸载政策。如果在执行块中使用可变状态数据或无法保存的其他数据，活动可以使用 <xref:System.Activities.NoPersistHandle> 向宿主指示不应保存它。工作流还可以使用 <xref:System.Activities.Statements.Persist> 活动将其数据显式保存到持久性存储介质中。