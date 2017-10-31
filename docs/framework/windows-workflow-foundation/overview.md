---
title: "Windows 工作流概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fc44adbe-1412-49ae-81af-0298be44aae6
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Windows 工作流概述
工作流是一组存储为模型的名为活动的基本单元，活动用于描述实际进程。工作流提供了一种方法，用于描述多项短期运行或长期运行的工作之间的执行顺序和依赖关系。此工作从头到尾地贯穿模型，并且活动可以人工执行或由系统功能执行。  
  
## 工作流运行时引擎  
 每个正在运行的工作流实例都是由进程内运行时引擎创建和维护的，宿主进程通过以下类之一与其交互：  
  
-   <xref:System.Activities.WorkflowInvoker>，它像调用方法一样调用工作流。  
  
-   <xref:System.Activities.WorkflowApplication>，用于对单个工作流实例的执行进行显式控制。  
  
-   <xref:System.ServiceModel.WorkflowServiceHost>，用于多实例方案中基于消息的交互。  
  
 上述每个类对表示为负责活动执行的 <xref:System.Activities.ActivityInstance> 的核心活动运行时进行包装。在一个应用程序域中可以并发运行多个 <xref:System.Activities.ActivityInstance> 对象。  
  
 上述三个宿主交互对象中的每一个都是从称为工作流程序的活动树中创建的。使用这些类型或对 <xref:System.Activities.ActivityInstance> 进行包装的自定义宿主，可以在包括控制台应用程序、基于窗体的应用程序、Windows 服务、[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 网站和 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务在内的任何 Windows 进程内执行工作流。  
  
 ![宿主进程中的工作流组件](../../../docs/framework/windows-workflow-foundation//media/44c79d1d-178b-4487-87ed-3e33015a3842.png "44c79d1d\-178b\-4487\-87ed\-3e33015a3842")  
宿主进程中的工作流组件  
  
## 工作流组件之间的交互  
 下图演示工作流组件彼此之间如何进行交互。  
  
 ![工作流交互](../../../docs/framework/windows-workflow-foundation//media/workflowinteraction.gif "WorkflowInteraction")  
  
 在前面的图中，<xref:System.Activities.WorkflowInvoker.Invoke%2A> 方法的 <xref:System.Activities.WorkflowInvoker> 类用于调用几个工作流实例。<xref:System.Activities.WorkflowInvoker> 用于不需要由宿主管理的轻型工作流；需要由宿主管理的工作流（如 <xref:System.Activities.Bookmark> 恢复）必须改用 <xref:System.Activities.WorkflowApplication.Run%2A> 来执行。无需等待一个工作流实例完成即可调用下一个工作流实例；运行时引擎支持同时运行多个工作流实例。调用的工作流如下：  
  
-   一个包含 <xref:System.Activities.Statements.WriteLine> 子活动的 <xref:System.Activities.Statements.Sequence> 活动。<xref:System.Activities.Variable> 的父活动是绑定到  <xref:System.Activities.InArgument> 的子活动。[!INCLUDE[crabout](../../../includes/crabout-md.md)] 变量、参数和绑定，请参见 [变量和参数](../../../docs/framework/windows-workflow-foundation//variables-and-arguments.md)。  
  
-   一个调用 `ReadLine` 的自定义活动。将 `ReadLine` 活动的 <xref:System.Activities.OutArgument> 返回给调用 <xref:System.Activities.WorkflowInvoker.Invoke%2A> 方法。  
  
-   一个派生自 <xref:System.Activities.CodeActivity> 抽象类的自定义活动。<xref:System.Activities.CodeActivity> 可以使用作为 <xref:System.Activities.CodeActivity.Execute%2A> 方法的参数提供的 <xref:System.Activities.CodeActivityContext> 访问运行时功能（如跟踪和属性）。[!INCLUDE[crabout](../../../includes/crabout-md.md)] 这些运行功能，请参见 [工作流跟踪](../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md) 和 [工作流执行属性](../../../docs/framework/windows-workflow-foundation//workflow-execution-properties.md)。  
  
## 请参阅  
 [BizTalk Server 2006 or WF?Choosing the Right Workflow Tool for Your Project](http://go.microsoft.com/fwlink/?LinkId=154901)