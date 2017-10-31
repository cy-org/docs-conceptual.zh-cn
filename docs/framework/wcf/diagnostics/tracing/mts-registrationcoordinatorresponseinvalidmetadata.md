---
title: "Microsoft.Transactions.TransactionBridge.RegistrationCoordinatorResponseInvalidMetadata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a174bbf5-0ffe-4fda-969d-e7fbd1996123
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.Transactions.TransactionBridge.RegistrationCoordinatorResponseInvalidMetadata
WS\-Atomic Transaction 协议服务接收到来自其协调程序的 RegisterResponse 消息，其中包含带有无效或不兼容元数据的终结点引用。  
  
## 说明  
 在本地事务管理器尝试向其上级事务管理器进行注册并且上级在 RegisterResponse 消息中返回无效地址时被跟踪。  
  
## 请参阅  
 [跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [使用跟踪来排除应用程序故障](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)