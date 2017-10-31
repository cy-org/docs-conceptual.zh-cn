---
title: "1148 - FlowchartSwitchCaseNotFound | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9ee7fcee-e040-4306-968e-ed840a1cb00c
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 1148 - FlowchartSwitchCaseNotFound
## 属性  
  
|||  
|-|-|  
|ID|1148|  
|关键字|WFActivities|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 指示在 Flowchart 开关中找不到匹配大小写，也找不到默认大小写。  Flowchart 执行将结束。  
  
## 消息  
 Flowchart“%1”\/FlowSwitch \- 找不到 Case 活动，也找不到与 Expression 结果匹配的 Default Case。  Flowchart 执行将结束。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|FlowChart|xs:string|FlowChart 的显示名称。|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|