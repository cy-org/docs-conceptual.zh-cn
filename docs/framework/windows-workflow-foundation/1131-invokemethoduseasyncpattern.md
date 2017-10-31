---
title: "1131 - InvokeMethodUseAsyncPattern | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eca50fa7-5276-4759-ad1c-e490b9bd1f82
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 1131 - InvokeMethodUseAsyncPattern
## 属性  
  
|||  
|-|-|  
|ID|1131|  
|关键字|WFRuntime|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 在 CacheMetadata 步骤中，InvokeMethod 活动指示它在调用方法时使用异步模式。  
  
## 消息  
 InvokeMethod“%1”\- 方法使用“%2”和“%3”的异步模式。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|InvokeMethod|xs:string|InvokeMethod 活动的显示名称。|  
|BeginMethod|xs:string|begin 方法的名称。|  
|EndMethod|xs:string|end 方法的名称。|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|