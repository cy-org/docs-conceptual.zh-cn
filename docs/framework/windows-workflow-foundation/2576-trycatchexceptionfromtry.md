---
title: "2576 - TryCatchExceptionFromTry | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 47e48973-b17c-4a16-8338-c84b54aa0a6e
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 2576 - TryCatchExceptionFromTry
## 属性  
  
|||  
|-|-|  
|ID|2576|  
|关键字|WFActivities|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 指示 TryCatch 活动捕获了异常。  
  
## 消息  
 TryCatch 活动“%1”捕获了“%2”类型的异常。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|DisplayName|xs:string|活动的显示名称。|  
|例外|xs:string|异常的类型名称。|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|