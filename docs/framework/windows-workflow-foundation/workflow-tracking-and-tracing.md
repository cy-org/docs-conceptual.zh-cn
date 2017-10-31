---
title: "工作流跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "编程 [WF], 跟踪"
ms.assetid: b965ded6-370a-483d-8790-f794f65b137e
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# 工作流跟踪
Windows 工作流跟踪是专为查看工作流执行情况而设计的一个 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 功能。它提供一个跟踪基础结构，用于跟踪工作流实例的执行。WF 跟踪基础结构透明地检测工作流以发出反应执行期间关键事件的记录。默认情况下，任何 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 工作流都可以使用此功能。不需要对 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]工作流进行任何更改即可进行跟踪。只需确定要接收的跟踪数据量。工作流实例开始或完成之后，会发出其处理跟踪记录。跟踪还可以提取与工作流变量关联的相关业务数据。例如，如果工作流表示一个订单处理系统，则可以提取 <xref:System.Activities.Tracking.TrackingRecord> 对象以及订单 ID。一般来讲，启用 WF 跟踪便于访问工作流执行的诊断数据或业务分析数据。  
  
 这些跟踪组件相当于 [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] 中的跟踪服务。在 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 中，WF 跟踪功能的性能已改进，其编程模型也已简化。跟踪运行时会检测工作流实例以发出与工作流生命周期和工作流活动有关的事件以及自定义事件。  
  
 Windows Server App Fabric 还提供了监视 WCF 和工作流服务的执行的能力。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Windows Server App Fabric 监控](http://go.microsoft.com/fwlink/?LinkId=201273) 和 [使用 Windows Server AppFabric 监控应用程序监控](http://go.microsoft.com/fwlink/?LinkId=201287)  
  
 若要对工作流运行时进行故障排除，则可以启用诊断工作流跟踪。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][工作流跟踪](../../../docs/framework/windows-workflow-foundation//workflow-tracing.md).  
  
 为了了解编程模型，本主题中介绍了跟踪基础结构的主要组件：  
  
-   从工作流运行时发出的 <xref:System.Activities.Tracking.TrackingRecord> 对象。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][跟踪记录](../../../docs/framework/windows-workflow-foundation//tracking-records.md).  
  
-   <xref:System.Activities.Tracking.TrackingParticipant> 对象订阅 <xref:System.Activities.Tracking.TrackingRecord> 对象。跟踪参与者包含用于处理 <xref:System.Activities.Tracking.TrackingRecord> 对象中负载的逻辑（例如，它们可以选择向某个文件写入）。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][跟踪参与者](../../../docs/framework/windows-workflow-foundation//tracking-participants.md).  
  
-   <xref:System.Activities.Tracking.TrackingProfile> 对象筛选从工作流实例发出的跟踪记录。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][跟踪配置文件](../../../docs/framework/windows-workflow-foundation//tracking-profiles.md).  
  
## 工作流跟踪基础结构  
 工作流跟踪基础结构遵循一个范例，即发布和订阅范例。工作流实例是跟踪记录的发布者，而跟踪记录的订阅者注册为工作流的扩展。订阅 <xref:System.Activities.Tracking.TrackingRecord> 对象的这些扩展称为跟踪参与者。跟踪参与者是一些扩展点，这些扩展点按照编写的目的来访问 <xref:System.Activities.Tracking.TrackingRecord> 对象和处理对象。跟踪基础结构允许对传出跟踪记录应用筛选器，以便参与者可订阅该记录的子集。此筛选机制是通过跟踪配置文件来实现的。  
  
 下图显示了跟踪基础结构的整体概况。  
  
 ![工作流跟踪基础结构](../../../docs/framework/windows-workflow-foundation//media/wv.gif "WV")  
  
## 本节内容  
 [跟踪记录](../../../docs/framework/windows-workflow-foundation//tracking-records.md)  
 介绍工作流运行时发出的跟踪记录。  
  
 [跟踪配置文件](../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)  
 介绍如何使用跟踪配置文件。  
  
 [跟踪参与者](../../../docs/framework/windows-workflow-foundation//tracking-participants.md)  
 介绍如何使用系统提供的跟踪参与者或如何创建自定义的跟踪参与者。  
  
 [为工作流配置跟踪](../../../docs/framework/windows-workflow-foundation//configuring-tracking-for-a-workflow.md)  
 介绍如何为工作流配置跟踪。  
  
 [工作流跟踪](../../../docs/framework/windows-workflow-foundation//workflow-tracing.md)  
 介绍为工作流启用调试跟踪的两种方法。  
  
 [使用跟踪确定工作流执行持续时间](../../../docs/framework/windows-workflow-foundation//determining-workflow-execution-duration-using-tracing.md)  
 描述如何使用跟踪消息决定工作流执行的持续时间。  
  
## 请参阅  
 [SQL 跟踪](../../../docs/framework/windows-workflow-foundation/samples/sql-tracking.md)