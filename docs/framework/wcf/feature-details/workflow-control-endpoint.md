---
title: "工作流控制终结点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1b883334-1590-4fbb-b0d6-65197efe0700
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 工作流控制终结点
开发人员可以使用工作流控制终结点调用控制操作，从而远程控制使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 承载的工作流实例。可以利用此功能以编程方式执行控制操作，如挂起、继续和终止。  
  
> [!WARNING]
>  如果在事务中使用工作流控制终结点且受控工作流包含 <xref:System.Activities.Statements.Persist> 活动，则工作流实例会挂起，直到事务超时。  
  
## 工作流实例管理  
 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]可定义名为 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> 的新协定。此协定将定义一系列控制操作，通过 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 这些控制操作可以远程控制由工作流实例的操作。<xref:System.ServiceModel.Activities.WorkflowControlEndpoint> 是提供的一种实现的标准终结点 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> 合同。<xref:System.ServiceModel.Activities.WorkflowControlClient> 是一个类，用于发送到控制操作 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>。  
  
 工作流实例可以是以下状态之一：  
  
 活动  
 工作流达到完成状态之前并且不处于挂起状态时的状态。在这种状态下，工作流实例运行并处理应用程序消息。  
  
 挂起  
 处于此状态时，即使有尚未开始运行或已部分运行的活动，工作流实例仍不运行。  
  
 完成  
 工作流实例的最终状态。工作流实例达到完成状态后，就无法再运行。  
  
## IWorkflowInstanceManagement  
 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> 接口将定义一组具有同步和异步版本的控制操作。事务处理版本要求使用识别事务处理的绑定。下表列出了支持的控制操作。  
  
|控制操作|说明|  
|----------|--------|  
|中止|强制停止执行工作流实例。|  
|取消|将工作流实例从活动或挂起状态转换为完成状态。|  
|运行|向工作流实例提供执行的机会。|  
|挂起|将工作流实例从活动状态转换为挂起状态。|  
|终止|将工作流实例从活动或挂起状态转换为完成状态。|  
|取消挂起|将工作流实例从挂起状态转换为活动状态。|  
|TransactedCancel|在某个事务（从客户端流入或在本地创建）下执行取消操作。如果系统维护了工作流实例的持久状态，则工作流实例必须在执行此操作期间存在。|  
|TransactedRun|在某个事务（从客户端流入或在本地创建）下执行运行操作。如果系统维护了工作流实例的持久状态，则工作流实例必须在执行此操作期间存在。|  
|TransactedSuspend|在某个事务（从客户端流入或在本地创建）下执行挂起操作。如果系统维护了工作流实例的持久状态，则工作流实例必须在执行此操作期间存在。|  
|TransactedTerminate|在某个事务（从客户端流入或在本地创建）下执行终止操作。如果系统维护了工作流实例的持久状态，则工作流实例必须在执行此操作期间存在。|  
|TransactedUnsuspend|在某个事务（从客户端流入或在本地创建）下执行取消挂起操作。如果系统维护了工作流实例的持久状态，则工作流实例必须在执行此操作期间存在。|  
  
 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> 协定无法用于创建新工作流实例，它只能管理现有工作流实例。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 远程创建新的工作流实例，请参阅 [工作流服务主机可扩展性](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)。  
  
## WorkflowControlEndpoint  
 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> 是具有固定协定 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> 的标准终结点。将此终结点添加到 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 实例，随后可以使用此终结点将命令操作发送到由宿主实例承载的任何工作流实例。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 标准终结点，请参见 [标准终结点](../../../../docs/framework/wcf/feature-details/standard-endpoints.md)。  
  
## WorkflowControlClient  
 <xref:System.ServiceModel.Activities.WorkflowControlClient> 是一个类，可用于将控制消息发送到位于 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 上的 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>。它包含为每个支持的操作的一种方法 <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> 合同的执行事务处理的操作除外。<xref:System.ServiceModel.Activities.WorkflowControlClient> 使用环境事务来确定是否应使用事务处理的操作。