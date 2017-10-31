---
title: "57398 - MaxInstancesExceeded | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f943d209-dfeb-43e5-b572-c9a06217936e
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 57398 - MaxInstancesExceeded
## 属性  
  
|||  
|-|-|  
|ID|57398|  
|关键字|WFServices|  
|级别|警告|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/分析|  
  
## 描述  
 指示系统达到为限制“MaxConcurrentInstances”设置的限制值。  
  
## 消息  
 系统达到为限制“MaxConcurrentInstances”设置的限制值。  此限制的限制值设置为 %1。  可通过修改 serviceThrottle 元素中的特性“maxConcurrentInstances”或修改行为 ServiceThrottlingBehavior 的“MaxConcurrentInstances”属性来更改限制值。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|名称|xs:string|项的名称。|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|