---
title: "System.ServiceModel.TxFailedToNegotiateOleTx | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f0f0b4b-a1ad-4704-8329-455daf54892d
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# System.ServiceModel.TxFailedToNegotiateOleTx
对指定协调上下文的 OleTransactions 协议协商失败。  
  
## 说明  
 当带有 OleTx 信息的传入事务无法使用附加的 OleTx 信息，将回退并改用 WS\-AT 时进行跟踪。  
  
## 疑难解答  
 指示计算机之间的 MSDTC RPC 通信所具有的一个潜在问题。如果日志中出现许多此类跟踪，则可能导致性能急剧下降。如果不希望使用 OleTx，请在 WS\-AT 注册表配置中将 `OleTxUpgradeEnabled` 设置为 0。  
  
## 请参阅  
 [跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [使用跟踪来排除应用程序故障](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)