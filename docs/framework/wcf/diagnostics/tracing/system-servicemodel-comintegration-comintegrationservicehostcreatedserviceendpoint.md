---
title: "System.ServiceModel.Channels.MsmqMoveOrDeleteAttemptFailed | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d75d39da-7502-4a6a-91b9-eaa05b8e24d5
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# System.ServiceModel.Channels.MsmqMoveOrDeleteAttemptFailed
无法移动或删除消息。  
  
## 描述  
 跟踪指示当尝试移动、删除或拒绝 MSMQ 消息时出错。  
  
 MSMQ 消息由 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 使用（当与 NetMsmqBinding 或 MsmqIntegrationBinding 一起使用时）。此跟踪与 NetMsmqBinding 或 MsmqIntegrationBinding 上的 `ReceiveErrorHandling` 属性的选定值相关。  
  
 此跟踪不会指示出全部的系统失败。  但是，它会指示某条消息的选定病毒消息处理失败。  有关消息何时成为病毒消息以及如何配置服务以适当地处理病毒消息的更多详细信息，请参见[病毒消息处理](http://go.microsoft.com/fwlink/?LinkID=99546)（可能为英文网页）。  
  
## 请参阅  
 [跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [使用跟踪来排除应用程序故障](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)