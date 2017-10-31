---
title: "PiiLoggingNotAllowed | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fc34a0b6-fee7-4da4-b146-b0c1c8b7519a
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# PiiLoggingNotAllowed
ID：108  
  
 严重性：错误  
  
 类别：跟踪  
  
## 描述  
 此事件指示没有正在记录的已知 PII。  不允许记录已知的 PII。  若要记录已知的 PII，请在 Machine.config 中将“enableLoggingKnownPii”设置为 `true`。  该事件将列出进程名称和进程 ID。  
  
## 请参阅  
 [事件日志记录](../../../../../docs/framework/wcf/diagnostics/event-logging/index.md)   
 [事件常规参考](../../../../../docs/framework/wcf/diagnostics/event-logging/events-general-reference.md)