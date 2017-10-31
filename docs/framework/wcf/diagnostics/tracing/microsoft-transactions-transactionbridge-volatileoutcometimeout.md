---
title: "Microsoft.Transactions.TransactionBridge.VolatileOutcomeTimeout | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2dbe34c5-57c7-4b64-9257-63021911d03c
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.Transactions.TransactionBridge.VolatileOutcomeTimeout
WS\-AT 协议服务在等待可变参与方对结果消息的响应时超时。如果参与方返回，则事务结果可能不确定。  
  
## 说明  
 当可变参与方已决定提交或中止，但未在给定时间内响应提交或回滚请求时跟踪。  
  
## 疑难解答  
 确保所有可变参与方都能在给定时间内响应。默认时间为 180 秒。如果此时间不够，请增加 WS\-AT 的 `VolatileOutcomeDelay` 计时器策略。  
  
## 请参阅  
 [跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [使用跟踪来排除应用程序故障](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)