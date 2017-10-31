---
title: "Analytic Tracing with ETW | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "diagnostics [WCF], analytic tracing"
  - "administration [WCF], analytic tracing"
  - "analytic tracing [WCF]"
ms.assetid: 1d518e47-a38d-41e8-93d7-8c3b361f6a56
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Analytic Tracing with ETW
[!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 解析跟踪提供一种方式来捕获的执行过程中的诊断信息 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务。[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 分析跟踪是在 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 堆栈中的关键点处发出的事件，用于在生产环境中排除 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务的故障。[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务的分析跟踪对承载 [!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)] [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务的产品服务器性能影响最小，因为这些事件可以非常高效地发送到 Windows 事件跟踪 \(ETW\) 会话。  
  
## 本节内容  
 [分析跟踪概述](../../../../../docs/framework/wcf/diagnostics/etw/analytic-tracing-overview.md)  
 讨论 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 分析跟踪如何在 [!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)] 中工作。  
  
 [动态启用分析跟踪](../../../../../docs/framework/wcf/diagnostics/etw/dynamically-enabling-analytic-tracing.md)  
 讨论如何使用 ETW 动态启用或禁用跟踪。  
  
 [配置消息流跟踪](../../../../../docs/framework/wcf/diagnostics/etw/configuring-message-flow-tracing.md)  
 描述如何配置消息流跟踪。  
  
 [分析跟踪事件参考](../../../../../docs/framework/wcf/diagnostics/etw/analytic-trace-event-reference.md)  
 显示一张表，其中包括事件 ID 及其事件级别、事件消息和关键字。  
  
## 请参阅  
 [针对 Windows 的 WCF 服务和事件跟踪](../../../../../docs/framework/wcf/samples/wcf-services-and-event-tracing-for-windows.md)   
 [在 Windows 事件跟踪中跟踪事件](../../../../../docs/framework/windows-workflow-foundation/samples/tracking-events-into-event-tracing-in-windows.md)