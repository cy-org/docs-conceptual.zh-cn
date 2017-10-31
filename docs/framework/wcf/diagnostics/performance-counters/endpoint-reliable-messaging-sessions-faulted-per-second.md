---
title: "终结点：Reliable Messaging Sessions Faulted Per Second（每秒出错的可靠消息会话数） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e9ae808a-7e1f-46b0-9560-d5a866be6d6e
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 终结点：Reliable Messaging Sessions Faulted Per Second（每秒出错的可靠消息会话数）
计数器名称：Reliable Messaging Sessions Faulted Per Second（每秒出错的可靠消息会话数）。  
  
## 描述  
 此终结点上每秒出错的可靠消息会话的数量。  
  
 此计数器为性能计数器类型 [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649)（可能为英文网页），可使用以下公式计算其值：  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)