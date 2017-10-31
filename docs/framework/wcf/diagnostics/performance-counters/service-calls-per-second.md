---
title: "服务：Calls Per Second（每秒调用次数） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6261d28d-d449-425a-b9fc-a4ee14079134
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 服务：Calls Per Second（每秒调用次数）
计数器名称：Calls Per Second（每秒调用次数）  
  
## 说明  
 一秒内调用此服务的次数。  
  
 此计数器为性能计数器类型 [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649)（可能为英文网页），可使用以下公式计算其值：  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\) 中分子 \(N\) 代表上一个取样时间间隔内完成的操作数。，分母 \(D\) 代表上一个取样时间间隔内记录的滴答数，而 F 则是滴答频率。