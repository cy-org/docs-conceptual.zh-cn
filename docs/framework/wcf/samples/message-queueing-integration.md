---
title: "消息队列集成 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d2b47a0-5d51-45b5-9633-b62e064e8ea4
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 消息队列集成
本节包含演示消息队列与 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 之间集成的示例。  
  
## 本节内容  
 [到 Windows Communication Foundation 的消息队列](../../../../docs/framework/wcf/samples/message-queuing-to-wcf.md)  
 演示消息队列 \(MSMQ\) 应用程序如何将 MSMQ 消息发送到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  
  
 [自定义多路分解器](../../../../docs/framework/wcf/samples/custom-demux.md)  
 演示如何将 MSMQ 消息头映射到不同服务操作，以便使用 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> 的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务不限于使用一个服务操作。  
  
 [Windows Communication Foundation 到消息队列](../../../../docs/framework/wcf/samples/wcf-to-message-queuing.md)  
 演示 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序如何将消息发送到消息队列 \(MSMQ\) 应用程序。  
  
 [消息相关性](../../../../docs/framework/wcf/samples/message-correlation.md)  
 演示在请求\/响应方案中，消息队列 \(MSMQ\) 应用程序如何将 MSMQ 消息发送到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，以及如何在发送方应用程序与接收方应用程序之间将消息关联起来。