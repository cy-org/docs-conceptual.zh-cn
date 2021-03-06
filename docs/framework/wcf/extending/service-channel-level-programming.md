---
title: "服务通道级编程 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d8dcd85-0a05-4c44-8861-4a0b3b90cca9
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 服务通道级编程
本主题介绍如何在不使用 <xref:System.ServiceModel.ServiceHost?displayProperty=fullName> 及其关联的对象模型的情况下编写 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务应用程序。  
  
## 接收消息  
 若要准备接收并处理消息，必须执行下列步骤：  
  
1.  创建绑定。  
  
2.  生成通道侦听器。  
  
3.  打开通道侦听器。  
  
4.  读取请求并发送答复。  
  
5.  关闭所有通道对象。  
  
#### 创建绑定  
 侦听和接收消息的第一步创建一个绑定。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 随附有几个可以直接通过实例化一个人使用的内置或系统提供的绑定。另外，您还可以创建自己的自定义绑定，方法是实例化 CustomBinding 类，这同时也是列表 1 中的代码所执行的操作。  
  
 下面的代码示例创建了 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName> 的一个实例，并将 <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=fullName> 添加到其 Elements 集合（这是用于生成通道堆栈的绑定元素的集合）。在此示例中，由于元素集合只有 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>，所以生成的通道堆栈仅具有 HTTP 传输通道。  
  
#### 生成 ChannelListener  
 在创建绑定后，我们调用 <xref:System.ServiceModel.Channels.Binding.BuildChannelListener%601%2A?displayProperty=fullName> 来生成通道侦听器，其中类型参数就是要创建的通道形状。在此示例中使用 <xref:System.ServiceModel.Channels.IReplyChannel?displayProperty=fullName>，这是因为我们希望以请求\/答复消息交换模式侦听传入的消息。  
  
 <xref:System.ServiceModel.Channels.IReplyChannel> 用于接收请求消息，并发回答复消息。调用 <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A?displayProperty=fullName> 会返回一个 <xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=fullName>，可以用于接收请求消息以及发回答复消息。  
  
 当创建侦听器时，我们传递发生侦听的网络地址，在此示例中为 `http://localhost:8080/channelapp`。通常，每个传输通道支持一个或可能多个地址方案，例如，HTTP 传输对 http 和 https 方案均予以支持。  
  
 在创建侦听器时，我们还传递空的 <xref:System.ServiceModel.Channels.BindingParameterCollection?displayProperty=fullName>。绑定参数是一种机制，用于传递那些控制侦听器生成方式的参数。在此示例中，我们不使用任何此类参数，所以我们传递的是一个空集合。  
  
#### 侦听传入消息  
 然后，我们对侦听器调用 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=fullName>，开始接受通道。<xref:System.ServiceModel.Channels.IChannelListener%601.AcceptChannel%2A?displayProperty=fullName> 的行为取决于传输是面向连接还是与连接无关。对于面向连接的传输，<xref:System.ServiceModel.Channels.IChannelListener%601.AcceptChannel%2A> 会一直阻止，直到新的连接请求传入（此时它会返回一个表示该新连接的新通道）。对于与连接无关的传输（如 HTTP），<xref:System.ServiceModel.Channels.IChannelListener%601.AcceptChannel%2A> 会立即返回传输侦听器创建的唯一通道。  
  
 在此示例中，侦听器返回一个实现 <xref:System.ServiceModel.Channels.IReplyChannel> 的通道。为了在此通道上接收消息，我们首先对其调用 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=fullName>，以便将其置于一个准备进行通信的状态。然后，我们调用 <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A>，它会处于阻止状态，直到消息达到。  
  
#### 读取请求并发送答复  
 当 <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A> 返回一个 <xref:System.ServiceModel.Channels.RequestContext>，我们使用其 <xref:System.ServiceModel.Channels.RequestContext.RequestMessage%2A> 属性获取收到的消息。我们写出消息的操作和正文内容（假设它是一个字符串）。  
  
 为了发送答复，我们在此例中创建一个新的答复消息，它会将我们在请求中收到的字符串数据传递回去。然后，我们调用 <xref:System.ServiceModel.Channels.RequestContext.Reply%2A> 以发送答复消息。  
  
#### 关闭对象  
 为避免泄漏资源，很重要的一点就是关闭通信中不再需要使用的对象。在此示例中，我们关闭了请求消息、请求上下文、通道和侦听器。  
  
 下面的代码示例演示通道侦听器仅接收一条消息所用的基本服务。实际的服务会一直接受通道及接收消息，直到服务退出。  
  
 [!code-csharp[ChannelProgrammingBasic#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/channelprogrammingbasic/cs/serviceprogram.cs#1)]
 [!code-vb[ChannelProgrammingBasic#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/channelprogrammingbasic/vb/serviceprogram.vb#1)]