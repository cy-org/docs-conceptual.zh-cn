---
title: "1124 - InvokeMethodIsStatic | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b9643641-fb52-4fa8-b354-4dd6617d68f6
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 1124 - InvokeMethodIsStatic
## 属性  
  
|||  
|-|-|  
|ID|1124|  
|关键字|WFRuntime|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 在 CacheMetadata 步骤中，InvokeMethod 活动指示要调用的方法是静态的。  
  
## 消息  
 InvokeMethod“%1”\- 方法为静态。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|InvokeMethod|xs:string|InvokeMethod 活动的显示名称。|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|