---
title: "System.ServiceModel.Channels.ConnectionPoolCloseException | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8358898e-129e-4fac-a6bf-bf3aa4293ae2
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# System.ServiceModel.Channels.ConnectionPoolCloseException
关闭此连接池中的连接时发生异常。  
  
## 说明  
 此错误级别跟踪指示当关闭由 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 的连接池功能使用的连接池时发生了错误。一种可能的原因是一个池连接或一组池连接在 CloseTimeout 内未成功关闭。当引发此异常时，将中止该池内所有剩余的未关闭连接，并放弃其他池内的未关闭连接。  
  
## 请参阅  
 [跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [使用跟踪来排除应用程序故障](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)