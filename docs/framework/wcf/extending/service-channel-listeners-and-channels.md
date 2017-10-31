---
title: "服务：通道侦听器和通道 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ccbe0e8-7e55-441d-80de-5765f67542fa
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 服务：通道侦听器和通道
共有三种类别的通道对象：通道、通道侦听器和通道工厂。通道是应用程序和通道堆栈之间的接口。通道侦听器负责在接收（即侦听）端创建通道，这通常是为了响应新传入的消息或连接。通道工厂负责在发送端创建通道，以便启动与终结点的通信。  
  
## 通道侦听器和通道  
 通道侦听器负责创建通道并从下面的层或者从网络接收消息。收到的消息将借助于通道侦听器所创建的通道传送到上面的层中。  
  
 下面的关系图阐释了接收消息并将其传送到上面的层的过程。  
  
 ![通道侦听器和通道](../../../../docs/framework/wcf/extending/media/wcfc-wcfchannelsigure1highlevelc.gif "wcfc\_WCFChannelsigure1HighLevelc")  
通道侦听器接收消息并借助于通道将收到的消息传送到上面的层。  
  
 该过程在概念上可建模为每个通道中的一个队列，尽管在具体实现中可能并不实际使用队列。通道侦听器负责从下面的层或者从网络接收消息，并将收到的消息放入队列。通道负责从队列中获取消息，并在上面的层请求消息（例如通过对通道调用 `Receive`）时将收到的消息传送到该层。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 为上述过程提供基类帮助器。（有关本主题中所讨论的通道帮助器类的关系图，请参见[通道模型概述](../../../../docs/framework/wcf/extending/channel-model-overview.md)。）  
  
-   <xref:System.ServiceModel.Channels.CommunicationObject> 类实现 <xref:System.ServiceModel.ICommunicationObject> 并强制执行[开发通道](../../../../docs/framework/wcf/extending/developing-channels.md)的步骤 2 中所述的状态机。  
  
-   <xref:System.ServiceModel.Channels.ChannelManagerBase> 类实现 <xref:System.ServiceModel.Channels.CommunicationObject> 并为 <xref:System.ServiceModel.Channels.ChannelFactoryBase> 和 <xref:System.ServiceModel.Channels.ChannelListenerBase> 提供统一的基类。<xref:System.ServiceModel.Channels.ChannelManagerBase> 类与 <xref:System.ServiceModel.Channels.ChannelBase>（用来实现 <xref:System.ServiceModel.Channels.IChannel> 的基类）结合使用。  
  
-   ``  <xref:System.ServiceModel.Channels.ChannelFactoryBase> 类实现 <xref:System.ServiceModel.Channels.ChannelManagerBase> 和 <xref:System.ServiceModel.Channels.IChannelFactory>，并将 `CreateChannel` 重载合并到一个 `OnCreateChannel` 抽象方法中。  
  
-   <xref:System.ServiceModel.Channels.ChannelListenerBase> 类实现 <xref:System.ServiceModel.Channels.IChannelListener>。它负责执行基本的状态管理。  
  
 下面的讨论基于[传输：UDP](../../../../docs/framework/wcf/samples/transport-udp.md) 示例。  
  
## 创建通道侦听器  
 该示例所实现的``UdpChannelListener 派生自 <xref:System.ServiceModel.Channels.ChannelListenerBase> 类。它使用单个 UDP 套接字来接收数据报。`OnOpen` 方法使用该 UDP 套接字来以异步循环形式接收数据。收到的数据随后将借助于消息编码系统转换为消息：  
  
```  
message = UdpConstants.MessageEncoder.ReadMessage(  
  new ArraySegment<byte>(buffer, 0, count),   
  bufferManager  
);  
```  
  
 由于可以用同一个数据报通道来表示源自许多源的消息，因此 `UdpChannelListener` 是一个单一实例侦听器。一次最多只能将一个活动的 <xref:System.ServiceModel.Channels.IChannel>``与该侦听器相关联。只有当随后释放了由 <xref:System.ServiceModel.Channels.ChannelListenerBase%601.AcceptChannel%2A> 方法返回的通道时，该示例才生成另一个通道。收到的消息将排入这个单一实例通道的队列中。  
  
### UdpInputChannel  
 `UdpInputChannel` 类实现 <xref:System.ServiceModel.Channels.IInputChannel>。该类由一个队列组成，该队列中包含多个由 `UdpChannelListener` 的套接字填充的传入消息。这些消息可以由 <xref:System.ServiceModel.Channels.IInputChannel.Receive%2A> 方法取消排队。