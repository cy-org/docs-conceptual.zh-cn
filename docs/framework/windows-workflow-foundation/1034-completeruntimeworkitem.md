---
title: "1034 - CompleteRuntimeWorkItem | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 45620011-8b04-4f87-ab5a-65b24145e17d
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 1034 - CompleteRuntimeWorkItem
## 属性  
  
|||  
|-|-|  
|ID|1034|  
|关键字|WFRuntime|  
|级别|详细|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 指示 RuntimeWorkItem 已完成。  
  
## 消息  
 Activity“%1”、DisplayName“%2”、InstanceId“%3”的运行时工作项已经完成。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|Activity|xs:string|活动的类型名称。|  
|DisplayName|xs:string|活动的显示名称。|  
|InstanceId|xs:string|活动的实例 ID。|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|