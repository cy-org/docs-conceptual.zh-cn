---
title: "1004 - WorkflowInstanceAborted | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: edb9ab8c-0b9a-488d-aa96-9c8c7984b53c
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 1004 - WorkflowInstanceAborted
## 属性  
  
|||  
|-|-|  
|ID|1004|  
|关键字|WFRuntime|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 指示工作流实例已中止并且具有异常。  
  
## 消息  
 WorkflowInstance Id“%1”因出现异常而中止。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|WorkflowInstanceId|`xs:string`|工作流的实例 ID|  
|例外|`xs:string`|异常的异常详细信息|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|