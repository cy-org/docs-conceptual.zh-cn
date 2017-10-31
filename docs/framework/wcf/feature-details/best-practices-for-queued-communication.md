---
title: "排队通信的最佳做法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "最佳做法 [WCF], 排队通信"
  - "队列 [WCF], 最佳做法"
ms.assetid: 446a6383-cae3-4338-b193-a33c14a49948
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 排队通信的最佳做法
本主题对 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的排队通信提供建议做法。以下各节从方案角度讨论建议的做法。  
  
## 快速、高效的排队消息处理  
 如果方案需要排队消息处理所提供的分离，还需要具有高效保证的快速、高性能消息处理，请使用非事务性队列并将 <xref:System.ServiceModel.MsmqBindingBase.ExactlyOnce%2A> 属性设置为 `false`。  
  
 此外，将 <xref:System.ServiceModel.MsmqBindingBase.Durable%2A> 属性设置为 `false`，还可以选择不产生磁盘写入开销。  
  
 安全性对性能有影响。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][性能注意事项](../../../../docs/framework/wcf/feature-details/performance-considerations.md).  
  
## 可靠的端对端排队消息处理  
 以下各节介绍的建议做法适用于要求进行端对端可靠消息处理的方案。  
  
### 基本可靠的传输  
 要实现端对端可靠性，请将 <xref:System.ServiceModel.MsmqBindingBase.ExactlyOnce%2A> 属性设置为 `true` 以确保传输安全。<xref:System.ServiceModel.MsmqBindingBase.Durable%2A> 属性可以设置为 `true` 或 `false`，具体取决于您的要求（默认值为 `true`）。作为端对端可靠性的一部分，<xref:System.ServiceModel.MsmqBindingBase.Durable%2A> 属性通常设置为 `true`。代价是性能损失，但可使消息持久，这样，即使队列管理器崩溃，消息也不会丢失。  
  
### 事务的使用  
 必须使用事务来确保端对端可靠性。`ExactlyOnce` 保证只能确保将消息传送到目标队列。若要确保接收到消息，请使用事务。如果不使用事务，在服务崩溃的情况下，将丢失虽然正在传递实际上已传送到应用程序的消息。  
  
### 死信队列的使用  
 死信队列可确保您在消息未能传递到目标队列时收到通知。您可以使用系统提供的死信队列，也可以使用自定义的死信队列。通常，最好使用自定义的死信队列，因为这样可以将死信消息从一个应用程序发送到单个死信队列。否则，系统上运行的所有应用程序产生的所有死信消息都会传递到单个队列。然后，每个应用程序都必须在该死信队列中搜索，寻找与自己相关的死信消息。有时，使用自定义死信队列并不可行，例如使用 MSMQ 3.0 时。  
  
 不建议为端对端可靠通信关闭死信队列。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [使用死信队列处理消息传输故障](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md).  
  
### 病毒消息处理的使用  
 通过病毒消息处理，可从消息处理失败的状态下恢复。  
  
 在使用病毒消息处理功能时，请确保将 <xref:System.ServiceModel.MsmqBindingBase.ReceiveErrorHandling%2A> 属性设置为适当的值。将该属性设置为 <xref:System.ServiceModel.ReceiveErrorHandling> 表示数据丢失。另一方面，如果该属性设置为 <xref:System.ServiceModel.ReceiveErrorHandling>，服务主机一旦检测到病毒消息，则被视为出现了错误。使用 MSMQ 3.0 时，最好使用 <xref:System.ServiceModel.ReceiveErrorHandling> 来避免数据丢失并移出病毒消息。使用 MSMQ 4.0 时，建议使用 <xref:System.ServiceModel.ReceiveErrorHandling>。<xref:System.ServiceModel.ReceiveErrorHandling> 将病毒消息移出队列，以便服务可以继续处理新消息。这样，病毒消息服务就可以单独处理病毒消息。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [病毒消息处理](../../../../docs/framework/wcf/feature-details/poison-message-handling.md).  
  
## 实现高吞吐量  
 若要在单个终结点上实现高吞吐量，请使用下面的方法：  
  
-   事务处理批处理。事务处理批处理可确保在单个事务中能够读取多个消息。这样可优化事务提交，从而提高整体性能。批处理的代价在于，如果一个批次内某个消息出现错误，则整个批次都会回滚，并且这些消息必须逐个处理，直到可以再次安全地进行批处理为止。大多数情况下，很少出现病毒消息，因此首选使用批处理来提高系统性能，尤其是具有参与事务的其他资源管理器时。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][在事务中对消息进行批处理](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md).  
  
-   并发。并发可增加吞吐量，但并发也会影响对共享资源的争用。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][并发](../../../../docs/framework/wcf/samples/concurrency.md).  
  
-   遏制。要实现最佳性能，需要遏制调度程序管线中的消息数。有关如何进行遏制的示例，请参见[遏制](../../../../docs/framework/wcf/samples/throttling.md)。  
  
 使用批处理时，应注意并发和遏制转换为并发批处理。  
  
 若要实现高吞吐量和可用性，请使用从队列中进行读取操作的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务场。这要求所有这些服务都在相同的终结点上公开相同的协定。场方法最适用于具有高消息产生率的应用程序，因为它使大量服务都从同一队列中进行读取操作。  
  
 使用场时，应注意 MSMQ 3.0 不支持远程事务处理读取。MSMQ 4.0 支持远程事务处理读取。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [在事务中对消息进行批处理](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md) 和 [Windows Vista、Windows Server 2003 和 Windows XP 在排队功能方面的差异](../../../../docs/framework/wcf/feature-details/diff-in-queue-in-vista-server-2003-windows-xp.md)。  
  
## 以工作语义为单元排队  
 某些情况下，队列中的一组消息可能具有相关性，因此这些消息的顺序很重要。在这些情况下，将一组相关消息作为单个单元进行处理：要么成功处理所有消息，要么所有消息的处理都不成功。若要实现这样的行为，请将会话用于队列。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [在会话中对排队消息进行分组](../../../../docs/framework/wcf/feature-details/grouping-queued-messages-in-a-session.md).  
  
## 关联请求\-回复消息  
 虽然队列一般是单向的，但在某些情况下，可能希望将接收到的回复关联到先前发送的请求。如果需要此类关联，建议应用自己的 SOAP 消息头，它包含消息的关联信息。通常，发送方将此标头附加到消息，接收方处理消息并在回复队列中用新消息回复时，会附加发送方的消息头，消息头包含关联信息，这样发送方就能通过请求消息识别出回复消息。  
  
## 集成非 WCF 应用程序  
 当集成 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务或客户端与非 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务或客户端时，可使用 `MsmqIntegrationBinding`。非 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序可以是一个使用 System.Messaging、COM\+、[!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 或 C\+\+ 编写的 MSMQ 应用程序。  
  
 使用 `MsmqIntegrationBinding` 时，应注意以下几点：  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息正文与 MSMQ 消息正文不同。使用排队绑定发送 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息正文置于 MSMQ 消息内。MSMQ 基础结构并不在意这一额外信息，它只注意 MSMQ 消息。  
  
-   `MsmqIntegrationBinding` 支持常见的序列化类型。根据序列化类型和一般消息的正文类型，<xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601> 采用不同的类型参数。例如，<xref:System.ServiceModel.MsmqIntegration.MsmqMessageSerializationFormat> 需要 `MsmqMessage\<byte[]>` 而 <xref:System.ServiceModel.MsmqIntegration.MsmqMessageSerializationFormat> 需要 `MsmqMessage<Stream>`。  
  
-   对于 XML 序列化，可以使用 `KnownTypes` 属性在 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) 元素上指定已知类型，然后使用该元素确定反序列化 XML 消息的方式。  
  
## 请参阅  
 [在 WCF 中排队](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)   
 [如何：使用 WCF 终结点交换排队消息](../../../../docs/framework/wcf/feature-details/how-to-exchange-queued-messages-with-wcf-endpoints.md)   
 [如何：与 WCF 终结点和消息队列应用程序交换消息](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)   
 [在会话中对排队消息进行分组](../../../../docs/framework/wcf/feature-details/grouping-queued-messages-in-a-session.md)   
 [在事务中对消息进行批处理](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md)   
 [使用死信队列处理消息传输故障](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md)   
 [病毒消息处理](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)   
 [Windows Vista、Windows Server 2003 和 Windows XP 在排队功能方面的差异](../../../../docs/framework/wcf/feature-details/diff-in-queue-in-vista-server-2003-windows-xp.md)   
 [使用传输安全保护消息](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md)   
 [使用消息安全保护消息](../../../../docs/framework/wcf/feature-details/securing-messages-using-message-security.md)   
 [排队消息处理疑难解答](../../../../docs/framework/wcf/feature-details/troubleshooting-queued-messaging.md)