---
title: "可靠会话概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: a7fc4146-ee2c-444c-82d4-ef6faffccc2d
caps.latest.revision: 30
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 30
---
# 可靠会话概述
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] SOAP 可靠消息传递提供 SOAP 终结点之间的端对端消息传输可靠性。此消息传递通过克服传输失败和 SOAP 消息级别失败，可在不可靠的网络上实现传输可靠性。具体而言，它为跨 SOAP 或传输中介发送的消息提供了一种基于会话的、单一的和（可选）有序的传送。基于对话的传送可按消息的顺序（可选）将消息分组到一个会话中。  
  
 下面将讨论什么是可靠会话、如何和何时使用可靠会话，以及如何保护可靠会话。  
  
## WCF 可靠会话  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠会话是一个如 WS\-ReliableMessaging 协议所定义的 SOAP 可靠消息传递的实现。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] SOAP 可靠消息传递提供两个终结点之间的端到端的可靠会话，而不管消息传递的终结点之间相隔的中介的数量或类型如何。这包括不使用 SOAP 的任何传输中介（例如 HTTP 代理）或在终结点之间流动所必需的使用 SOAP 的中介（例如基于 SOAP 的路由器或网桥）。可靠会话通道支持“交互式”通信，因此通过这类通道连接的服务可以并发运行，并可以在低延迟的条件下（即，在相对较短的时间间隔内）交换和处理消息。这种耦合意味着这些组件将同时成功或同时失败，因此它们之间没有提供隔离。  
  
 可靠会话可以屏蔽两种失败情况：  
  
-   SOAP 消息级失败，其中包括消息丢失或重复的情况以及消息到达的顺序与消息发送的顺序不同的情况。  
  
-   传输失败。  
  
 可靠会话实现 WS\-ReliableMessaging 协议和内存中传输窗口以屏蔽 SOAP 消息级失败，并在传输失败的情况下重新建立连接。  
  
 可靠会话为 SOAP 消息提供 TCP 为 IP 数据包提供的内容。TCP 套接字连接在节点之间提供单个的 IP 数据包有序传输。可靠通道提供相同类型的可靠传输，但在以下方面与 TCP 套接字可靠性不同：  
  
-   可靠性位于 SOAP 消息级别，而不是针对一个任意大小的字节数据包。  
  
-   可靠性是非传输特定的，而不仅仅是针对通过 TCP 的传输。  
  
-   可靠性不与特定的传输会话（例如，TCP 连接提供的会话）相关联，并可以在可靠会话的生存期中以并发或顺序方式使用多个传输会话。  
  
-   可靠会话是发送方和接收方的 SOAP 终结点之间的会话，与二者之间的连接所需的传输连接的数目无关。简而言之，TCP 可靠性在传输连接结束的位置结束，而可靠会话提供端到端的可靠性。  
  
## 可靠会话和绑定  
 如前所述，可靠会话是非传输特定的，因此可以在许多传输上实现。此外，可以通过许多消息交换模式建立可靠会话，例如请求\-答复或双工模式。因此，可将 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠会话作为一组绑定的属性进行公开。  
  
 可以在使用以下内容的终结点上使用可靠会话：  
  
-   基于 HTTP 的传输协议标准绑定：  
  
    -   `WsHttpBinding` 并公开请求\-答复或单向协定。  
  
    -   对请求\-答复或简单的单向服务协定使用可靠会话时可以使用。  
  
    -   `WsDualHttpBinding` 并公开双工、请求\-答复或单向协定。  
  
    -   `WsFederationHttpBinding` 并公开请求\-答复或单向协定。  
  
-   基于 TCP 的传输协议标准绑定：  
  
    -   `NetTcpBinding` 并公开双工、请求答复或单向协定。  
  
 通过创建自定义绑定（例如 HTTPS，有关问题的更多信息，请参见本主题后面的“可靠会话和安全”部分）或命名管道绑定，还可以在任何其他绑定上使用可靠会话。  
  
 可以在不同的基础通道类型上堆栈可靠会话，并且生成的可靠会话通道形状将会不同。在客户端和服务器上，支持的可靠会话通道的类型取决于所使用的基础通道的类型。下表列出了在客户端上作为基础通道的一项功能支持的会话通道的类型。  
  
|支持的可靠会话通道类型（给定基础通道类型的情况下支持的 `TChannel` 值）|`IRequestChannel`|`IRequestSessionChanne`l|`IDuplexChannel`|`IDuplexSessionChannel`|  
|-----------------------------------------------|-----------------------|------------------------------|----------------------|-----------------------------|  
|`IOutputSessionChannel`|是|是|是|是|  
|`IRequestSessionChannel`|是|是|否|否|  
|`IDuplexSessionChannel`|否|否|是|是|  
  
 支持的通道类型是可用于传入到 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.BuildChannelFactory%60%601%28System.ServiceModel.Channels.BindingContext%29> 方法的泛型 `TChannel` 参数值的值。  
  
 下表列出了在服务器上作为基础通道的一项功能支持的会话通道的类型。  
  
|支持的可靠会话通道类型（给定基础通道类型的情况下支持的 `TChannel` 值）|`IReplyChannel`|`IReplySessionChannel`|`IDuplexChannel`|`IDuplexSessionChannel`|  
|-----------------------------------------------|---------------------|----------------------------|----------------------|-----------------------------|  
|`IInputSessionChannel`|是|是|是|是|  
|`IReplySessionChannel`|是|是|否|否|  
|`IDuplexSessionChannel`|否|否|是|是|  
  
 支持的通道类型是可用于传入到 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.BuildChannelListener%60%601%28System.ServiceModel.Channels.BindingContext%29> 方法的泛型 `TChannel` 参数值的值。  
  
## 可靠会话和安全  
 保护可靠会话的安全很重要，这可以确保对通信方（服务和客户端）进行身份验证以及在会话中交换的消息不会被篡改。而且，必须确保每个单独的可靠会话的完整性。通过将可靠会话绑定到由安全会话通道表示和管理的安全上下文，可以保护可靠会话。安全通道提供安全会话。然后，使用在会话建立的过程中交换的安全令牌保护可靠会话中的消息。  
  
 当可靠会话是通过 TCP\-S 进行时，TCP 会话与可靠会话相关联，因此，传输安全确保安全也与可靠会话相关联。在此情况下，将关闭重新建立连接的操作。  
  
 唯一的例外是在使用 HTTPS 时。安全套接字层 \(SSL\) 会话未绑定到可靠会话。这会造成某种安全威胁，这是因为共享安全上下文（SSL 会话）的会话彼此之间不设防，根据不同的应用程序，这可能是也可能不是一种真正的安全威胁。  
  
## 使用可靠会话  
 若要使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠会话，请使用支持可靠会话的绑定创建一个终结点。使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的一种启用可靠会话的、系统提供的绑定，或创建可完成此操作的自定义绑定。默认情况下支持并启用可靠会话的系统定义的绑定包括：  
  
-   <xref:System.ServiceModel.WSDualHttpBinding>  
  
 支持可靠会话（作为选项）但默认情况下不启用可靠会话的系统提供的绑定包括：  
  
-   <xref:System.ServiceModel.WSHttpBinding>  
  
-   <xref:System.ServiceModel.WSFederationHttpBinding>  
  
-   <xref:System.ServiceModel.NetTcpBinding>  
  
 有关如何创建自定义绑定的示例，请参见[如何：创建使用 HTTPS 的自定义可靠会话绑定](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-reliable-session-binding-with-https.md)。  
  
 有关支持可靠会话的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 绑定的讨论，请参见[系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)。  
  
## 使用可靠会话的场合  
 了解何时在应用程序中使用可靠会话是很重要的。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持同时处于活动状态并在生命期内的终结点之间的可靠会话。如果应用程序要求一个终结点在某个持续时间内不可用，则可以使用列队实现可靠性。  
  
 如果方案要求两个终结点通过 TCP 进行连接，那么 TCP 也许足以提供可靠消息交换，而没有必要使用可靠会话；TCP 可确保数据包按顺序到达并且只到达一次。  
  
 如果方案具有以下任何特征，则必须认真地考虑使用可靠会话：  
  
-   SOAP 中介，例如 SOAP 路由器。  
  
-   代理中介或传输桥。  
  
-   连接时好时坏。  
  
-   通过 HTTP 传输的会话。  
  
## 请参阅  
 [使用绑定配置服务和客户端](../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [WS 可靠会话](../../../../docs/framework/wcf/samples/ws-reliable-session.md)