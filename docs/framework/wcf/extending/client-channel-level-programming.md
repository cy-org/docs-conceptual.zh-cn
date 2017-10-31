---
title: "客户端通道级编程 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3b787719-4e77-4e77-96a6-5b15a11b995a
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 客户端通道级编程
本主题介绍如何在不使用 <xref:System.ServiceModel.ClientBase%601?displayProperty=fullName> 类及其关联的对象模型的情况下编写 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 客户端应用程序。  
  
## 发送消息  
 若要准备发送消息并接收和处理回复，需要执行下列步骤：  
  
1.  创建绑定。  
  
2.  生成通道工厂。  
  
3.  创建通道。  
  
4.  发送请求并读取回复。  
  
5.  关闭所有通道对象。  
  
#### 创建绑定  
 与接收的情况类似（请参见[服务通道级编程](../../../../docs/framework/wcf/extending/service-channel-level-programming.md)），发送消息是从创建绑定开始。本示例创建一个新的 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName> 并将一个 <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=fullName> 添加到其 Elements 集合中。  
  
#### 生成 ChannelFactory  
 这次我们不创建 <xref:System.ServiceModel.Channels.IChannelListener?displayProperty=fullName>，而是通过调用类型参数为 <xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=fullName> 的绑定上的 <xref:System.ServiceModel.ChannelFactory.CreateFactory%2A?displayProperty=fullName> 来创建一个 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=fullName>。当等待传入消息的一方使用通道侦听器时，发起通信以创建通道的一方将使用通道工厂。和通道侦听器相似，必须先打开通道工厂之后才能使用通道工厂。  
  
#### 创建通道  
 然后我们调用 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=fullName> 来创建一个 <xref:System.ServiceModel.Channels.IRequestChannel>。此调用接受我们要使用创建的新通道与之通信的终结点的地址。得到通道后，我们调用它的 Open 以使其处于通信就绪状态。根据传输的性质，这次对 Open 的调用可能发起与目标终结点的连接，或者在网络上根本不执行任何操作。  
  
#### 发送请求并读取回复  
 打开通道之后，可以创建消息并使用通道的 Request 方法发送请求并等待回复返回。当此方法返回时，我们将得到回复消息，可以读取该消息以发现终结点回复的内容。  
  
#### 关闭对象  
 为避免泄漏资源，我们将关闭通信中不再需要使用的对象。  
  
 下面的代码示例演示了一个基本客户端使用通道工厂发送消息并读取回复。  
  
 [!code-csharp[ChannelProgrammingBasic#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/channelprogrammingbasic/cs/clientprogram.cs#2)]
 [!code-vb[ChannelProgrammingBasic#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/channelprogrammingbasic/vb/clientprogram.vb#2)]