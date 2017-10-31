---
title: "216 - MessageSentByTransport | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 150c3167-4154-4225-8d94-57cc94341233
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 216 - MessageSentByTransport
## 属性  
  
|||  
|-|-|  
|ID|216|  
|关键字|疑难解答，ServiceModel|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/分析|  
  
## 说明  
 使用基于 TCP 的传输发送消息时发生此事件。请注意，在传输级别上，单个操作可在客户端和服务之间交换多条消息。这可能是由于基础结构行为的特点，在此方面，安全性是一个很好的例子。因此，发出的 **MessageSentByTransport** 事件数随服务绑定及其配置而变化。  
  
## 消息  
 传输向“%1”发送了一条消息。  
  
## 详细信息  
  
|数据项名称|数据项类型|说明|  
|-----------|-----------|--------|  
|DestinationAddress|`xs:string`|将请求消息发送到的地址。|  
|HostReference|xs:string|对于 Web 承载的服务，此字段唯一标识 Web 层次结构中的服务。此字段的格式定义为“网站名称应用程序虚拟路径&#124;服务虚拟路径&#124;服务名称”。示例：“默认网站\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService”。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|