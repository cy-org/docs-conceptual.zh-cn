---
title: "1003 - WorkflowInstanceCanceled | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 64754dc2-c160-4bf3-869a-13d56694e2dc
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 1003 - WorkflowInstanceCanceled
## 属性  
  
|||  
|-|-|  
|ID|1003|  
|关键字|WFRuntime|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 指示工作流实例在“已取消”状态下完成。  
  
## 消息  
 WorkflowInstance Id“%1”在“已取消”状态下完成。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|WorkflowInstanceId|`xs:string`|工作流的实例 ID|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|