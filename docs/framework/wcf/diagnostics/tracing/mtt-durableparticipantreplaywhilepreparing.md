---
title: "Microsoft.Transactions.TransactionBridge.DurableParticipantReplayWhilePreparing | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 10ef3876-6f8e-4d4e-8444-f47847b64795
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.Transactions.TransactionBridge.DurableParticipantReplayWhilePreparing
WS\-AT 协议服务从不响应 Prepare 的持久参与者接收到重播消息。因此，中止了事务。  
  
## 说明  
 如果持久参与者仍然在准备时接收到重播消息，则进行跟踪。这是此状态的非法消息，将中止事务。  
  
## 疑难解答  
 收到此错误表示持久参与者（包括从属事务管理器）已从故障中恢复，但不确定事务结果，因此请求提供其状态。  
  
## 请参阅  
 [跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [使用跟踪来排除应用程序故障](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)