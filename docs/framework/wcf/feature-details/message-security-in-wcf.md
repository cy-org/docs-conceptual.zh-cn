---
title: "WCF 中的消息安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a80efb59-591a-4a37-bb3c-8fffa6ca0b7d
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# WCF 中的消息安全
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 有两个用于提供安全性的主要模式（`Transport` 和 `Message`），以及结合了这两者的第三个模式 \(`TransportWithMessageCredential`\)。本主题讨论消息安全和使用它的原因。  
  
## 何为消息安全？  
 消息安全使用 WS\-Security 规范来保护消息。WS\-Securityspecification 描述 SOAP 消息传送的增强功能，以在 SOAP 消息级（而非传输级）确保保密性、完整性和身份验证。  
  
 简言之，消息安全与传输安全的不同之处在于，前者将安全凭据和声明与每条消息以及任何消息保护（签名或加密）封装在一起。通过修改消息内容将安全直接应用于消息，受保护的消息可以在安全方面进行自包含。这会使某些在使用传输安全时不可能的情况成为可能。  
  
## 使用消息安全的原因  
 在消息级安全中，所有安全信息均封装在消息中。使用消息级安全（而非传输级安全）保护消息具有以下优点：  
  
-   端对端安全。传输安全（如安全套接字层 \(SSL\)）仅在通信是点对点时保护消息。如果消息在到达最终接收方之前要路由到一个或多个 SOAP 中介（例如，路由器），则一旦中介从网络上读取消息，消息本身将不会受到保护。此外，客户端身份验证信息仅对第一个中介可用，而且必须以带外方式重新传输到最终接收方（如果需要）。即使整个路由在单个跃点之间使用 SSL 安全也是如此。因为消息安全直接作用于消息并保护其中的 XML，所以无论消息在到达最终接收方之前涉及到多少中介，消息总能保持安全。这可以实现真正的端对端安全方案。  
  
-   增强的灵活性。可以对消息的某些部分（而非整个消息）进行签名或加密。这表示中介可以查看消息中为它们提供的那些部分。如果发送方需要让消息中的部分信息对中介可见，但又希望确保消息不被篡改，则它可以只对消息进行签名而不加密。由于签名属于消息，因而最终接收方可以验证消息中的信息是否按原样接收的。在某个方案中，可能有一个 SOAP 中介服务，该服务根据 Action 标头值路由消息。默认情况下，如果使用消息安全，则 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不加密 Action 值但对其进行签名。因此，所有中介都可获得此信息，但没有一个能更改它。  
  
-   对多个传输的支持。可以通过许多不同的传输（例如命名管道和 TCP）来发送受保护的消息，而不必依赖于安全协议。使用传输级安全时，所有安全信息的范围限定于单个特殊的传输连接，不能从消息内容本身获取这些信息。无论您使用什么传输来传送消息，消息安全都会让消息变得安全，并且安全上下文直接嵌入消息内。  
  
-   对一组范围广泛的凭据和声明的支持。消息安全基于 WS\-Security 规范，该规范提供能够在 SOAP 消息内传输任何类型声明的可扩展框架。与传输安全不同，您可以使用的这组身份验证机制或声明不受传输能力的限制。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息安全包括多种类型的身份验证和声明传输，并且可以根据需要进行扩展以支持其他类型。例如，由于这些原因，联合凭据方案不能没有消息安全。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]联合方案 WCF 支持的更多信息，请参见[联合令牌与颁发的令牌](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)。  
  
## 消息安全与传输安全比较  
  
### 传输级安全的优缺点  
 传输安全具有以下优点：  
  
-   不要求通信双方理解 XML 级安全概念。这可提高互操作性，例如，当将 HTTPS 用于保护通信时。  
  
-   全面提高的性能。  
  
-   提供了硬件加速器。  
  
-   可以使用流。  
  
 传输安全具有以下缺点：  
  
-   仅支持跃点到跃点。  
  
-   有限且不可扩展的凭据集。  
  
-   依赖于传输。  
  
### 消息级安全的缺点  
 消息安全具有以下缺点：  
  
-   性能  
  
-   不能使用消息流。  
  
-   要求实现 XML 级安全机制并支持 WS\-Security 规范。这可能影响互操作性。  
  
## 请参阅  
 [保护服务和客户端的安全](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [传输安全](../../../../docs/framework/wcf/feature-details/transport-security.md)   
 [如何：使用传输安全和消息凭据](../../../../docs/framework/wcf/feature-details/how-to-use-transport-security-and-message-credentials.md)   
 [Microsoft Patterns and Practices, Chapter 3: Implementing Transport and Message Layer Security（《Microsoft 模式与实践》第 3 章：实现传输和消息层安全性）](http://go.microsoft.com/fwlink/?LinkId=88897)