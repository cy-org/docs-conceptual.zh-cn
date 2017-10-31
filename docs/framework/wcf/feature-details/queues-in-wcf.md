---
title: "Windows Communication Foundation 中的队列 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "队列 [WCF]"
ms.assetid: 43008409-1bb4-4bd4-85d7-862c8f10ae20
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Windows Communication Foundation 中的队列
本节中的主题讨论 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 队列支持。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通过利用 Microsoft 消息队列（以前称为 MSMQ）作为传输机制来提供队列支持，支持以下方案：  
  
-   松耦合应用程序。发送应用程序可以将消息发送到队列，而无需知道接收应用程序是否可用于处理该消息。队列提供了处理独立性，它允许发送应用程序将消息以一定的速率发送到队列，该速率不依赖于接收应用程序的消息处理速度。如果向队列发送消息的操作与消息处理的操作不是紧密耦合的，则会提高系统的整体可用性。  
  
-   故障隔离。应用程序与队列之间发送或接收消息如果失败，两种操作互不影响。例如，如果接收应用程序失败，发送应用程序可以继续向队列发送消息。接收方再次启动时，即可处理队列中的消息。故障隔离提高了整体系统的可靠性和可用性。  
  
-   负载调节。发送应用程序发出的消息可能使接收应用程序过载。队列可以管理不匹配的消息生成率和处理率，以使接收方不会过载。  
  
-   断开连接的操作。在高延迟网络或有限可用性网络上通信（例如，在移动设备中）时，发送、接收和处理操作可能会断开连接。队列允许这些操作继续执行，即使终结点断开连接也是如此。重新建立连接后，队列将消息转发到接收应用程序。  
  
 若要在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序中使用队列功能，可以使用一个标准绑定，如果标准绑定不符合要求，也可以创建自定义绑定。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]相关标准绑定和如何选择标准绑定的更多信息，请参见[如何：与 WCF 终结点和消息队列应用程序交换消息](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]创建自定义绑定的更多信息，请参见[自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md)。  
  
## 本节内容  
 [队列概述](../../../../docs/framework/wcf/feature-details/queues-overview.md)  
 消息队列概念概述。  
  
 [在 WCF 中排队](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 队列支持概述。  
  
 [如何：使用 WCF 终结点交换排队消息](../../../../docs/framework/wcf/feature-details/how-to-exchange-queued-messages-with-wcf-endpoints.md)  
 说明如何使用 <xref:System.ServiceModel.NetMsmqBinding> 类在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务之间进行通信。  
  
 [如何：与 WCF 终结点和消息队列应用程序交换消息](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)  
 说明如何使用 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 和消息队列应用程序之间进行通信。  
  
 [在会话中对排队消息进行分组](../../../../docs/framework/wcf/feature-details/grouping-queued-messages-in-a-session.md)  
 说明如何对队列中的消息分组，以便单个接收应用程序加速处理相关消息。  
  
 [在事务中对消息进行批处理](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md)  
 说明如何在事务中对消息进行批处理。  
  
 [使用死信队列处理消息传输故障](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md)  
 说明如何使用死信队列来处理消息传输和传送故障，以及如何处理死信队列中的消息。  
  
 [病毒消息处理](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)  
 说明如何处理病毒消息（向接收应用程序尝试传送的次数超出最大次数的消息）。  
  
 [Windows Vista、Windows Server 2003 和 Windows XP 在排队功能方面的差异](../../../../docs/framework/wcf/feature-details/diff-in-queue-in-vista-server-2003-windows-xp.md)  
 总结 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 队列功能在 [!INCLUDE[wv](../../../../includes/wv-md.md)]、[!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 和 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 之间的区别。  
  
 [使用传输安全保护消息](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md)  
 介绍如何使用传输安全来保护排队消息。  
  
 [使用消息安全保护消息](../../../../docs/framework/wcf/feature-details/securing-messages-using-message-security.md)  
 介绍如何使用消息安全来保护排队消息。  
  
 [排队消息处理疑难解答](../../../../docs/framework/wcf/feature-details/troubleshooting-queued-messaging.md)  
 说明如何解决常见队列问题。  
  
 [排队通信的最佳做法](../../../../docs/framework/wcf/feature-details/best-practices-for-queued-communication.md)  
 说明使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 排队通信的最佳做法。  
  
## 请参阅  
 [Message Queuing](http://msdn.microsoft.com/zh-cn/ff917e87-05d5-478f-9430-0f560675ece1)