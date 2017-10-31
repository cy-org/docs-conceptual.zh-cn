---
title: "3502 - InferredOperationDescription | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6aebb614-3c72-4537-ba11-3cc7200ef1f1
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 3502 - InferredOperationDescription
## 属性  
  
|||  
|-|-|  
|ID|3502|  
|关键字|WFServices|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/分析|  
  
## 描述  
 指示已从 WorkflowService 中推断出 OperationDescription。  
  
## 消息  
 已从 WorkflowService 中推断出协定“%2”中含有 Name\='%1' 的 OperationDescription。  IsOneWay\=%3。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|OperationName|xs:string|操作的名称。|  
|ContractName|xs:string|协定的名称。|  
|IsOneWay|xs:string|true 或 false 指示协定是否为单向。|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|