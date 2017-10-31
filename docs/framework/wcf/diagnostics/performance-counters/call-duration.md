---
title: "Call Duration（调用持续时间） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e4973ec3-3c66-4c0b-b5d0-294b62c83f7d
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Call Duration（调用持续时间）
计数器名称：Call Duration（调用持续时间）  
  
## 描述  
 调用该操作的平均持续时间。  平均持续时间根据此公式计算：\(N1\-N0\)\/\(D1\-D0\)。  
  
> [!WARNING]
>  当用于异步 WCF 服务时，Call Duration（调用持续时间）计数器将始终返回 \-1。  
  
## 请参阅  
 [PERF\_AVERAGE\_TIMER](http://go.microsoft.com/fwlink/?LinkId=95015)