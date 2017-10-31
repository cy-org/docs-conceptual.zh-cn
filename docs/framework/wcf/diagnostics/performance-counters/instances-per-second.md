---
title: "每秒实例数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 74579397-1058-4278-80cf-2d00854a480f
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 每秒实例数
计数器名称：Instances Created Per Second（每秒创建的实例数）。  
  
## 说明  
 每秒创建的服务实例的总数。  
  
 此计数器为性能计数器类型 [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649)，可使用以下公式计算其值：  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)