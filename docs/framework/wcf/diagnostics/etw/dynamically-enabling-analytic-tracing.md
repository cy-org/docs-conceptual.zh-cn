---
title: "动态启用分析跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58b63cfc-307a-427d-b69d-9917ff9f44ac
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 动态启用分析跟踪
通过 Windows 操作系统附带的工具，可以使用 Windows 事件跟踪 \(ETW\) 动态启用或禁用跟踪。 对于所有 [!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)] [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 服务，可以动态启用和禁用分析跟踪，而无需修改应用程序的 Web.config 文件或重新启动服务。 这样，发出跟踪事件的应用程序就可以保持原样。  
  
 可以采用类似方式配置 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 跟踪选项。 例如，可以将严重性级别从 **Error** 更改为 **Information** 而不影响应用程序。 可以使用以下工具来实现此功能：  
  
-   **Logman** – 一个命令行工具，用于配置、控制和查询跟踪数据。[!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)][Logman Create Trace](http://go.microsoft.com/fwlink/?LinkId=165426)（Logman 创建跟踪）和 [Logman Update Trace](http://go.microsoft.com/fwlink/?LinkId=165427)（Logman 更新跟踪）。  
  
-   **EventViewer** \- Windows 图形管理工具，用于查看跟踪的结果。[!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)][针对 Windows 的 WCF 服务和事件跟踪](../../../../../docs/framework/wcf/samples/wcf-services-and-event-tracing-for-windows.md)和 [Event Viewer](http://go.microsoft.com/fwlink/?LinkId=165428)（事件查看器）。  
  
-   **Perfmon** – Windows 图形管理工具，它使用计数器监视跟踪计数器以及跟踪对性能的影响。[!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)][Create a Data Collector Set Manually](http://go.microsoft.com/fwlink/?LinkId=165429)（手动创建数据收集器集）。  
  
### 关键字  
 使用 <xref:System.ServiceModel.Activation.Configuration.ServiceModelActivationSectionGroup.Diagnostics%2A> 类时，通常按严重性级别（如 Error、Warning 和 Information）筛选 .NET Framework 跟踪消息。 ETW 支持严重性级别概念，但引入了使用关键字的新型灵活筛选器机制。 关键字为任意文本值，用于使跟踪事件提供有关事件含义的附加上下文。  
  
 对于 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 分析跟踪，每个跟踪事件都有两种关键字。 首先，每个事件包含一个或多个方案关键字。 这类关键字表示此事件将支持的各方案。 有三个方案关键字，每一个方案关键字均设计用于特定用途，如下表所示。 可以动态更改使用关键字进行的筛选而不会干扰 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务。 这意味着您可以动态更改当前跟踪方案以及所收集的跟踪信息量。 例如，您可以将 `HealthMonitoring` 更改为 `Troubleshooting`，并增加跟踪事件粒度。  
  
|关键字|描述|  
|---------|--------|  
|`HealthMonitoring`|非常轻量、程度最低的跟踪，用于监视服务活动。|  
|`EndToEndMonitoring`|用于支持消息流跟踪的事件。|  
|`Troubleshooting`|围绕 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 扩展点的粒度更细的事件。|  
  
 第二组关键字定义 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 的哪个组件发出了事件。  
  
|关键字|描述|  
|---------|--------|  
|`UserEvents`|由用户代码而非 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 发出的事件。|  
|`ServiceModel`|由 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 运行时发出的事件。|  
|`ServiceHost`|由服务主机发出的事件。|  
|`WCFMessageLogging`|[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 消息日志记录事件。|  
  
## 请参阅  
 [针对 Windows 的 WCF 服务和事件跟踪](../../../../../docs/framework/wcf/samples/wcf-services-and-event-tracing-for-windows.md)