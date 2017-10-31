---
title: "213 - ServiceHostStarted | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a6f7facc-342f-46bb-9d52-a470178ba6bb
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 213 - ServiceHostStarted
## 属性  
  
|||  
|-|-|  
|ID|213|  
|关键字|EndToEndMonitoring，HealthMonitoring，疑难解答，ServiceHost|  
|级别|LogAlways|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/分析|  
  
## 说明  
 在启动 Web 承载的服务主机时发出此事件。这通常在消息激活服务时发生。如果将服务配置为自动启动，也可能发生此事件。  
  
## 消息  
 ServiceHost 已启动:“%1”。  
  
## 详细信息  
  
|数据项名称|数据项类型|说明|  
|-----------|-----------|--------|  
|服务类型名称|`xs:string`|服务实现的类型的 CLR FullName。|  
|HostReference|`xs:string`|对于 Web 承载的服务，此字段唯一标识 Web 层次结构中的服务。此字段的格式定义为“网站名称应用程序虚拟路径&#124;服务虚拟路径&#124;服务名称”。示例：“默认网站\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService”。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|