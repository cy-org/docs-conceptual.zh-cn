---
title: "303 - UserDefinedInformationEventOccured | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5ed5acaf-3755-4417-92c4-4ebc8e854ca1
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 303 - UserDefinedInformationEventOccured
## 属性  
  
|||  
|-|-|  
|ID|303|  
|关键字|疑难解答，HealthMonitoring，UserEvents，ServiceModel，EndToEndMonitoring|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/分析|  
  
## 说明  
 此事件从用户代码发出。当开发人员的服务中出现自定义的信息性事件时，开发人员可以发出此事件。可以使用 <xref:System.Diagnostics.Eventing> API 完成此操作。此外，还提供了一个 WCF 示例，该示例包装 API 并演示如何正确发出此事件。  
  
## 消息  
 Name“%1”、Reference“%2”、Payload: %3  
  
## 详细信息  
  
|数据项名称|数据项类型|说明|  
|-----------|-----------|--------|  
|名称|`xs:string`|事件的用户定义名称|  
|HostReference|`xs:string`|对于 Web 承载的服务，此字段唯一标识 Web 层次结构中的服务。此字段的格式定义为“网站名称应用程序虚拟路径&#124;服务虚拟路径&#124;服务名称”。示例：“默认网站\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService”。|  
|Payload|`xs:string`|事件的用户定义负载。|