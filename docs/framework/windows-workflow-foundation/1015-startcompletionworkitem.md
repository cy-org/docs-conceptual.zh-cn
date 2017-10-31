---
title: "1015 - StartCompletionWorkItem | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 96fd1d4e-c5d0-46ad-8a71-4b4b49ac7262
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 1015 - StartCompletionWorkItem
## 属性  
  
|||  
|-|-|  
|ID|1015|  
|关键字|WFRuntime|  
|级别|详细|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 指示 CompletionWorkItem 正在开始执行。  
  
## 消息  
 开始为父 Activity“%1”、DisplayName“%2”、InstanceId“%3”执行 CompletionWorkItem。  已完成的活动“%4”、DisplayName：“%5”、InstanceId：“%6”。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|ParentActivity|xs:string|父活动的类型名称。|  
|ParentDisplayName|xs:string|父活动的显示名称。|  
|ParentInstanceId|xs:string|父活动的实例 ID。|  
|CompletedActivity|xs:string|已完成活动的类型名称。|  
|CompletedActivityDisplayName|xs:string|已完成活动的显示名称。|  
|CompletedActivityInstanceId|xs:string|已完成活动的实例 ID。|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|