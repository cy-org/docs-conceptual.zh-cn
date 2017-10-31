---
title: "System.ServiceModel.Channels.MsmqMessageRejected | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9b7c10a7-2af6-44a2-8b1a-90bba0c7cf26
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# System.ServiceModel.Channels.MsmqMessageRejected
MSMQ 已拒绝该消息。  
  
## 说明  
 此跟踪指示已拒绝 MSMQ 消息。  
  
 当 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)]（与 NetMsmqBinding 或 MsmqIntegrationBinding 一起使用时）无法处理 MSMQ 消息时可以拒绝这些消息。这些消息称为病毒消息。当 NetMsmqBinding 或 MsmqIntegrationBinding 上的 `ReceiveErrorHandling` 属性设置为 `Reject` 时，将拒绝病毒消息。拒绝的消息将会发送回发送方的 [Dead\-Letter Queue](http://go.microsoft.com/fwlink/?LinkID=99544)（死信队列）。  
  
 有关消息何时成为病毒消息以及如何配置服务以适当地处理病毒消息的更多详细信息，请参见[病毒消息处理](http://go.microsoft.com/fwlink/?LinkID=99546)（可能为英文网页）。  
  
 有关 MSMQ 中已拒绝消息的含义的更多详细信息，请参见 [MQMarkMessageRejected](http://go.microsoft.com/fwlink/?LinkID=99548)。  
  
## 请参阅  
 [跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [使用跟踪来排除应用程序故障](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)   
 [Poison\-Message Handling（病毒消息处理）](http://go.microsoft.com/fwlink/?LinkID=99546)   
 [MQMarkMessageRejected](http://go.microsoft.com/fwlink/?LinkID=99548)