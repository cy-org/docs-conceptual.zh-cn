---
title: "可靠会话的最佳做法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b94f6e01-8070-40b6-aac7-a2cb7b4cb4f2
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 可靠会话的最佳做法
本节讨论可靠会话的最佳实践。  
  
## 设置 MaxTransferWindowSize  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的可靠会话使用传输窗口保存客户端和服务上的消息。  可配置属性 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxTransferWindowSize%2A> 指示传输窗口可以保存多少条消息。  
  
 在发送方，这指示在等待确认消息时传输窗口可以保存多少条消息，在接收方，则指示为服务缓冲多少条消息。  
  
 选择合适的大小可影响使用网络的效率以及运行服务的最佳容量。  以下各节将详细介绍选择此属性的值时要考虑的事宜以及值的影响。  
  
 默认传输窗口大小是 8 条消息。  
  
### 有效使用网络  
 此处的“网络”一词对应于在客户端（发送方）和服务（接收方）之间用作通信基础的任何事物。  这包括传输连接以及中间的任何中介或者网桥，包括 SOAP 路由器或 HTTP 代理\/防火墙。  
  
 有效使用网络可确保充分利用网络容量。  可通过网络每秒传输的数据量（称为“数据速率”）以及从发送方到接收方传输数据所用的时间（称为“延迟”）都会影响利用网络的有效性。  
  
 在发送方，属性 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxTransferWindowSize%2A> 指示在等待确认消息时，其传输窗口可以保存多少条消息。  因此，如果网络延迟时间很长，为确保及时响应发送者和网络有效利用，应增加传输窗口大小。  
  
 例如，即使发送方满足数据速率，如果发送方和接收方之间存在多个中介或者中介或网络存在损失，则延迟时间会很长。  因此，在发送方接受要在网络上发送的新消息之前，必须在其传输窗口中等待消息的确认信息。  具有高延迟的缓冲区越小，网络利用率就越低。  另一方面，传输窗口大小过高可能会影响服务，原因是服务可能需要满足客户端的高发送速率。  
  
### 满负荷运行服务  
 为最大程度地有效使用网络，理想情况是服务也按最佳容量运行。  接收方上的传输窗口大小属性指示接收方可以缓冲多少条消息。  此消息缓冲不仅帮助网络流控制，而且还可让服务满负荷运行。  例如，如果缓冲区是 1，而且消息到达的速度超过了服务可以处理的速度，则网络可能会丢弃一些消息，并可能浪费或闲置网络容量。  
  
 使用缓冲区可提高服务的可用性，因为服务可以在处理以前接收到的消息的同时并发接收和缓冲消息。  
  
 建议您在发送方和接收方使用相同的 `MaxTransferWindowSize`。  
  
### 启用流控制  
 流控制是确保发送方和接收方互相保持步调一致的机制，也就是说，使用和处理消息的速度与产生消息的速度一样快。  客户端和服务上的传输窗口大小可确保发送方和接收方在一个合理的同步窗口中。  
  
 当在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务之间使用可靠会话时，强烈建议将 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled%2A> 属性设置 true。  
  
## 设置 MaxPendingChannels  
 当编写一个允许从不同的客户端启用可靠会话通信的服务时，可能会有许多客户端同时建立与该服务的可靠会话。  在这些情况下，服务的响应取决于 `MaxPendingChannels` 属性。  
  
 当发送方创建到接收方的可靠会话通道时，发送方和接收方之间的握手将建立可靠会话。  建立可靠会话之后，该通道会放入到挂起的通道队列中以供服务接受。  此 `MaxPendingChannels` 属性指示有多少个通道可以处于此状态。  
  
 服务有可能会处于一种无法接收更多通道的状态。  如果队列已满，则会拒绝建立可靠会话的尝试，客户端必须重试。  
  
 队列中挂起的通道也可能会在队列中保持很长时间。  此外，可能会出现可靠会话的非活动超时，从而导致通道转换到错误状态。  
  
 因此，在编写同时服务于多个客户端的服务时，应设置一个适合于您的需要的值。  为 `MaxPendingChannels` 属性设置过高的值会影响工作集。  
  
 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxPendingChannels%2A> 的默认值为 4。  
  
## 可靠会话和宿主  
 在为使用可靠会话服务提供 Web 宿主时，应该记住下面的重要注意事项：  
  
-   可靠会话是有状态的，而状态在 AppDomain 中进行维护。  这意味着，属于可靠会话的一部分的所有消息必须在同一个 AppDomain 中进行处理。  其大小超过 1 的网络场和网络园无法保证满足此约束。  
  
-   使用双工 HTTP 通道（例如使用 `WsDualHttpBinding`）的可靠会话会要求多于默认的每个客户端 2 个 HTTP 连接的连接数。  这意味着，双工可靠会话会在每个方向上要求 2 个连接，因为并发应用程序和协议消息可能会在任意给定时间在每个方向上进行传输。  这意味着，在某些特定的条件下，根据消息交换服务模式的不同，使用双工 HTTP 和可靠会话的 Web 承载服务可能会出现死锁。  若要增加每个客户端允许的 HTTP 连接数，请将下列代码添加到相关配置文件中（例如，相关服务的 web.config）：  
  
```  
<configuration>  
   <system.net>  
      <connectionManagement>  
         <add name = "*" maxconnection = "XX" />  
      </connectionManagement>  
   </system.net>  
</configuration>  
```  
  
 其中，“XX”是需要的连接数。  在此例中最小应为 4。