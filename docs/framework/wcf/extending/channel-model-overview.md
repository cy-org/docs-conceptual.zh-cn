---
title: "通道模型概述 | Microsoft Docs"
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
  - "通道模型 [WCF]"
ms.assetid: 07a81e11-3911-4632-90d2-cca99825b5bd
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 通道模型概述
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 通道堆栈是具有一个或多个消息处理通道的分层的通信堆栈。堆栈底部是传输通道，它负责使通道堆栈适应基础传输（例如，TCP、HTTP、SMTP 和其他类型的传输）。通道为消息的发送和接收提供了一个低级编程模型。此编程模型依赖于多个接口和其他类型模型（统称为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通道模型）。本主题讨论通道形状、基本通道侦听器（在服务上）和通道工厂（在客户端上）的构造。  
  
## 通道堆栈  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点使用一种称为通道堆栈的通信堆栈与世界通信。下图对通道堆栈和其他通信堆栈（如 TCP\/IP）进行了比较。  
  
 ![通道模型](../../../../docs/framework/wcf/extending/media/wcfc-channelstackhighlevelc.gif "wcfc\_ChannelStackHighLevelc")  
  
 首先说明共同点：在两种情况下，堆栈的每一层均提供该层下面一层的一些抽象，并仅向其上的一层公开该抽象。每一层只使用其下面一层的抽象。而且在这两种情况下，两个堆栈通信时，每个层均与另一个堆栈中的相应层通信，例如，IP 层与 IP 层通信，TCP 层与 TCP 层通信，依此类推。  
  
 现在说明区别：TCP 堆栈旨在提供物理网络的抽象，而通道堆栈不仅提供消息传送方式（即传输）的抽象，还提供其他功能（比如消息的内容或通信所使用的协议，包括但不仅仅限于传输）的抽象。例如，可靠的会话绑定元素是通道堆栈的一部分，但却不在传输下面或传输本身中。此抽象是通过要求堆栈中的底部通道使基础传输协议适应通道堆栈体系结构，然后依赖堆栈中更上层的通道提供通信功能（比如可靠性保证和安全）来实现的。  
  
 消息作为 <xref:System.ServiceModel.Channels.Message> 对象流过通信堆栈。如上图所示，底部通道称为传输通道。它是负责与其他方之间发送和接收消息的通道。这包括负责在与用于和其他方通信的格式之间转换 <xref:System.ServiceModel.Channels.Message> 对象。传输通道上面可以有任意个协议通道，每个协议通道负责提供一种通信功能（如可靠的传递保证）。协议通道对以 <xref:System.ServiceModel.Channels.Message> 对象的形式流过其中的消息执行操作。协议通道通常会转换消息（例如，通过添加标头或加密正文），或者发送和接收协议通道自己的控制消息（例如回执确认）。  
  
## 通道形状  
 每个通道均实现一个或多个接口，称为通道形状接口或通道形状。这些通道形状提供面向通信的方法（如通道实现的发送和接收或请求和答复）和通道调用的用户。通道形状的最底部是 <xref:System.ServiceModel.Channels.IChannel> 接口，该接口提供一个 `GetProperty`\<T\> 方法，用作访问由堆栈中的通道公开的任意功能的分层机制。扩展 <xref:System.ServiceModel.Channels.IChannel> 的五种通道形状为：  
  
-   <xref:System.ServiceModel.Channels.IInputChannel>  
  
-   <xref:System.ServiceModel.Channels.IOutputChannel>  
  
-   <xref:System.ServiceModel.Channels.IRequestChannel>  
  
-   <xref:System.ServiceModel.Channels.IReplyChannel>  
  
-   <xref:System.ServiceModel.Channels.IDuplexChannel>  
  
 另外，这些形状中的每个形状均有一个扩展 <xref:System.ServiceModel.Channels.ISessionChannel%601?displayProperty=fullName> 以支持会话的等效项。这些等效项是：  
  
-   <xref:System.ServiceModel.Channels.IInputSessionChannel>  
  
-   <xref:System.ServiceModel.Channels.IOutputSessionChannel>  
  
-   <xref:System.ServiceModel.Channels.IRequestSessionChannel>  
  
-   <xref:System.ServiceModel.Channels.IReplySessionChannel>  
  
-   <xref:System.ServiceModel.Channels.IDuplexSessionChannel>  
  
 在现有的传输协议支持某些基本消息交换模式后，通道形状可以实现模式化。例如，单向消息传递对应于一个 <xref:System.ServiceModel.Channels.IInputChannel>\/<xref:System.ServiceModel.Channels.IOutputChannel> 对，请求\-答复对应于 <xref:System.ServiceModel.Channels.IRequestChannel>\/<xref:System.ServiceModel.Channels.IReplyChannel> 对，双向双工通信对应于 <xref:System.ServiceModel.Channels.IDuplexChannel>（同时扩展 <xref:System.ServiceModel.Channels.IInputChannel> 和 <xref:System.ServiceModel.Channels.IOutputChannel>）。  
  
## 通道堆栈的编程  
 通道堆栈通常是使用工厂模式创建的，在这种模式中，绑定创建通道堆栈。在发送端，使用绑定生成 <xref:System.ServiceModel.ChannelFactory>，而后者生成通道堆栈并返回对堆栈中顶部通道的引用。之后，应用程序可以使用此通道发送消息。有关更多信息，请参见[客户端通道级编程](../../../../docs/framework/wcf/extending/client-channel-level-programming.md)。  
  
 在接收端，使用绑定生成 <xref:System.ServiceModel.Channels.IChannelListener>，用于侦听传入消息。<xref:System.ServiceModel.Channels.IChannelListener> 通过创建通道堆栈并将应用程序引用传递给顶部通道，将消息提供给侦听应用程序。之后，应用程序使用此通道接收传入消息。有关更多信息，请参见[服务通道级编程](../../../../docs/framework/wcf/extending/service-channel-level-programming.md)。  
  
## 通道对象模型  
 通道对象模型是实现通道、通道侦听器和通道工厂所必需的一组核心接口。还提供一些基类以辅助自定义实现。  
  
 通道侦听器负责侦听传入消息，然后通过由通道侦听器创建的通道将这些消息传送到上面的层。  
  
 通道工厂负责创建通道，这些通道用于发送消息，并在通道工厂关闭时，关闭通道工厂创建的所有通道。  
  
 <xref:System.ServiceModel.ICommunicationObject> 是定义的所有通信对象实现的基本状态机的核心接口。<xref:System.ServiceModel.Channels.CommunicationObject> 提供其他信道类可不必接口而不是从这个核心接口的实现。但这并不是必需的：自定义通道可以直接实现 <xref:System.ServiceModel.ICommunicationObject> 而不继承自 <xref:System.ServiceModel.Channels.CommunicationObject>。图 3 中的任何类都不是通道模型的部分；它们是想要生成通道的自定义通道实施者可以使用的帮助器。  
  
 ![通道模型](../../../../docs/framework/wcf/extending/media/wcfc-wcfcchannelsigure3omumtreec.gif "wcfc\_WCFCChannelsigure3OMUMTreec")  
  
 以下主题说明通道对象模型以及可帮助生成自定义通道的各个开发领域。  
  
|主题|说明|  
|--------|--------|  
|[服务：通道侦听器和通道](../../../../docs/framework/wcf/extending/service-channel-listeners-and-channels.md)|说明用于侦听服务应用程序中传入通道的通道侦听器。|  
|[客户端：通道工厂和通道](../../../../docs/framework/wcf/extending/client-channel-factories-and-channels.md)|说明用于创建通道以连接到服务应用程序的通道工厂。|  
|[了解状态更改](../../../../docs/framework/wcf/extending/understanding-state-changes.md)|说明 <xref:System.ServiceModel.ICommunicationObject?displayProperty=fullName> 接口如何模拟通道中的状态变化。|  
|[选择消息交换模式](../../../../docs/framework/wcf/extending/choosing-a-message-exchange-pattern.md)|说明通道可以支持的六种基本消息交换模式。|  
|[处理异常和错误](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md)|说明如何处理自定义通道中的错误和异常。|  
|[配置和元数据支持](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md)|说明如何支持从应用程序模型中使用自定义通道以及如何使用绑定和绑定元素导出和导入元数据。|