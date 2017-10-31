---
title: "219 - ServiceException | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 81e2efac-39aa-4ed2-85a9-97eb8793b844
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 219 - ServiceException
## 属性  
  
|||  
|-|-|  
|ID|219|  
|关键字|EndToEndMonitoring，HealthMonitoring，疑难解答，ServiceModel|  
|级别|错误|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/分析|  
  
## 说明  
 当 WCF 服务遇到未经处理的异常时会发出此事件。这包括在激活和消息处理期间以及在用户代码中出现的未经处理的异常。  
  
## 消息  
 消息处理过程中出现了“%2”类型的未经处理的异常。完整异常 ToString: %1。  
  
## 详细信息  
  
|数据项名称|数据项类型|说明|  
|-----------|-----------|--------|  
|ExceptionToString|`xs:string`|对 CLR 异常调用 `ToString`\(\) 的结果。|  
|ExceptionTypeName|`xs:string`|异常的类型的 CLR FullName。|  
|HostReference|`xs:string`|对于 Web 承载的服务，此字段唯一标识 Web 层次结构中的服务。此字段的格式定义为“网站名称应用程序虚拟路径&#124;服务虚拟路径&#124;服务名称”。示例：“默认网站\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService”。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|