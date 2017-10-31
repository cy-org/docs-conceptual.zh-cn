---
title: "每秒拒绝的排队消息数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77ea9aa3-b9e2-4a1d-a65e-5ca115ba0567
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 每秒拒绝的排队消息数
计数器名称：Queued Messages Rejected Per Second（每秒拒绝的排队消息数）。  
  
## 说明  
 此服务中每秒被排队传输拒绝的消息数。  
  
 此计数器为性能计数器类型 [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649),可使用以下公式计算其值：  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)