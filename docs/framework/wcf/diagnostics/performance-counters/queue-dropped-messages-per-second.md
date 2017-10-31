---
title: "每秒丢弃的排队消息数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 74540f52-8762-4147-b5ba-e171180515a3
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 每秒丢弃的排队消息数
计数器名称：Queued Messages Dropped Per Second（每秒丢弃的排队消息数）。  
  
## 说明  
 此服务处的排队传输机制每秒丢弃的消息数。  
  
 此计数器为性能计数器类型 [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649)，可使用以下公式计算其值：  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)