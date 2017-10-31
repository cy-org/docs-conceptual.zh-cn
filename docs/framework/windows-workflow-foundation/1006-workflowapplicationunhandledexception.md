---
title: "1006 - WorkflowApplicationUnhandledException | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dfe0f316-e03b-47fb-b6a3-622c56bfd753
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 1006 - WorkflowApplicationUnhandledException
## 属性  
  
|||  
|-|-|  
|ID|1006|  
|关键字|WFRuntime|  
|级别|错误|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 指示工作流应用程序遇到了未经处理的异常。  
  
## 消息  
 WorkflowInstance Id“%1”遇到了未经处理的异常。该异常来自 Activity“%2”、DisplayName“%3”。将进行以下操作: %4。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|WorkflowInstanceId|`xs:string`|工作流的实例 ID|  
|例外|`xs:string`|异常的异常详细信息|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|