---
title: "System.ServiceModel.Channels.MsmqPoisonMessageRejected | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e64b9bd-1f12-43df-a189-d7be3c2bace1
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# System.ServiceModel.Channels.MsmqPoisonMessageRejected
拒绝的病毒消息。  
  
## 说明  
 该跟踪指示遇到病毒消息并随后将其拒绝。当 NetMsmqBinding 或 MsmqIntegrationBinding 上的 `ReceiveErrorHandling` 属性设置为 `Reject` 时，将会出现此情况。拒绝的消息将会发送回发送方的 [Dead\-Letter Queue](http://go.microsoft.com/fwlink/?LinkId=99544)（死信队列）。  
  
 有关消息何时成为病毒消息以及如何配置服务以适当地处理病毒消息的更多详细信息，请参见[病毒消息处理](http://go.microsoft.com/fwlink/?LinkId=99546)（可能为英文网页）。有关 MSMQ 中已拒绝消息的含义的更多详细信息，请参见 [MQMarkMessageRejected](http://go.microsoft.com/fwlink/?LinkId=99548)。  
  
## 请参阅  
 [跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [使用跟踪来排除应用程序故障](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)   
 [病毒消息处理](http://go.microsoft.com/fwlink/?LinkId=99546)   
 [MQMarkMessageRejected](http://go.microsoft.com/fwlink/?LinkId=99548)