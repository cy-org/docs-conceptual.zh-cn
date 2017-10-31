---
title: "4207 - MaximumRetriesExceededForSqlCommand | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8c8bee26-9ad4-4e01-bd16-0e1fd510fb6b
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 4207 - MaximumRetriesExceededForSqlCommand
## 属性  
  
|||  
|-|-|  
|ID|4207|  
|关键字|配额，FInstanceStore|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 指示 SQL 提供程序正在放弃重试 SQL 命令，因为执行次数已达到了允许的最多重试次数。  
  
## 消息  
 正在放弃重试 SQL 命令，因为执行次数已达到了允许的最多重试次数。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|