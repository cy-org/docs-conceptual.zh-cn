---
title: "分析跟踪概述 | Microsoft Docs"
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
  - "分析跟踪 [WCF], 概述"
ms.assetid: ae55e9cc-0809-442f-921f-d644290ebf15
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# 分析跟踪概述
[!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)]中的分析跟踪是基于 Windows 事件跟踪 \(ETW\) 的高性能、低详细级别的跟踪功能。 ETW 在内核级别运行，极大地减少了跟踪操作的开销。 它有效缓冲用户模式和内核模式的事件，并允许动态启用日志记录，而无需重新启动服务。 发出并接收跟踪数据之后，即可在事件日志中获取这些数据。  
  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)] ETW，请参阅 [Improve Debugging and Performance Tuning with ETW](http://go.microsoft.com/fwlink/?LinkId=164781)（使用 ETW 改善调试和性能优化）。  
  
 除使用 Windows 的“系统”、“安全性”和“应用程序”事件日志分析应用程序外，[!INCLUDE[wv](../../../../../includes/wv-md.md)] 和 [!INCLUDE[lserver](../../../../../includes/lserver-md.md)] 还在“应用程序和服务日志”顶级节点下引入了其他日志。 这些新日志的用途在于存储特定应用程序或特定组件的事件，而不是存储具有系统范围影响的全局事件（如“安全性”事件日志可能记录的事件类型）。[!INCLUDE[netfx_current_short](../../../../../includes/netfx-current-short-md.md)] 将 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 跟踪事件的日志记录、[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 消息日志和 [!INCLUDE[wf1](../../../../../includes/wf1-md.md)] 跟踪记录统一和关联到应用程序和服务日志。  
  
## 概念和功能  
 下面的概念和功能适用于 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 分析跟踪。  
  
### 启用 WCF 诊断设置  
 WCF 诊断是在 \<system.serviceModel\>\<\>diagnostics 配置节中启用的。  
  
```  
  
<system.serviceModel>  
  <diagnostics>  
  
```  
  
 Web 承载的 IIS 虚拟应用程序的 WCF 诊断设置在该应用程序的 Web.config 文件中启用。 另一选择是在应用程序的子目录中创建 Web.config。  此选择会将这些设置应用于子目录中的所有服务。  若要确保对应用程序中的所有服务以一致的方式初始化诊断设置，诊断设置应位于应用程序目录中的 Web.config 内，而不是位于应用程序的其中一个单独子目录中。  
  
### 信道  
 ETW 允许软件组件利用通道将跟踪事件定向到特定用户。 例如，您可以将面向系统管理员的事件发送到一个通道，而将应用程序开发人员关注的事件发送到另一个通道。 通道在 Windows 中命名和注册，因此使用者可以使用事件查看器查看通道的事件。  
  
 适用于 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 中的 [!INCLUDE[netfx_current_short](../../../../../includes/netfx-current-short-md.md)] 的分析跟踪功能写入到 Microsoft\-Windows\-应用程序服务器\-应用程序通道。 此通道专门设计用于希望监视生产中 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务运行状况的用户。 它定义了一组少量事件，可用于多种运行状况监视和疑难解答情况。  
  
 若要针对 Windows 清单启用事件跟踪以便在事件日志中对消息正确解码，请在命令行上使用 ServiceModelReg 工具，如下所示：  
  
 `ServiceModelReg.exe -i -c:etw`  
  
### 动态配置  
 ETW 基础结构允许使用标准 Windows 工具动态启用和配置跟踪。[!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)][动态启用分析跟踪](../../../../../docs/framework/wcf/diagnostics/etw/dynamically-enabling-analytic-tracing.md).  
  
### 消息流跟踪  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)]如何启用消息流跟踪，请参阅[配置消息流跟踪](../../../../../docs/framework/wcf/diagnostics/etw/configuring-message-flow-tracing.md)。  
  
### 关键字  
 关键字用于筛选跟踪消息以及定义已发出事件的 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 组件。[!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [动态启用分析跟踪](../../../../../docs/framework/wcf/diagnostics/etw/dynamically-enabling-analytic-tracing.md).