---
title: "204 - ClientParameterInspectorBeforeCallInvoked | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8253555a-9002-4565-8ede-33d7a33a895f
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 204 - ClientParameterInspectorBeforeCallInvoked
## 属性  
  
|||  
|-|-|  
|ID|204|  
|关键字|疑难解答，ServiceModel|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/分析|  
  
## 说明  
 服务模型在客户端参数检查器上调用 `BeforeCall` 方法之后，将发出此事件。  
  
## 消息  
 调度程序对“%1”类型的 ClientParameterInspector 调用了“BeforeCall”。  
  
## 详细信息  
  
|数据项名称|数据项类型|说明|  
|-----------|-----------|--------|  
|TypeName|`xs:string`|所调用检查器的类型的 CLR FullName。|  
|HostReference|`xs:string`|对于 Web 承载的服务，此字段唯一标识 Web 层次结构中的服务。此字段的格式定义为“网站名称应用程序虚拟路径&#124;服务虚拟路径&#124;服务名称”。示例：“默认网站\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService”。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|