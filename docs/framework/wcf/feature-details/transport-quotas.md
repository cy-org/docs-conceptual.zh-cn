---
title: "传输配额 | Microsoft Docs"
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
  - "传输配额 [WCF]"
ms.assetid: 3e71dd3d-f981-4d9c-9c06-ff8abb61b717
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 传输配额
传输配额是一种策略机制，用于决定连接何时正在占用过多资源。配额是一种硬性限制，它在超出配额值时立即禁止使用其他资源。传输配额可防止恶意或无意的拒绝服务攻击。  
  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 传输的默认配额值基于资源的保守分配。这些默认值适合于开发环境和小型安装方案。如果某个安装耗尽了资源或是连接受到限制，则无论是否还有其他资源可用，服务管理员都应检查传输配额并调整各个配额值。  
  
## 传输配额的类型  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 传输具有三种类型的配额：  
  
-   “超时”可减少通过长时间占用资源来实施的拒绝服务攻击。  
  
-   “内存分配限制”可防止单个连接耗尽系统内存并拒绝为其他连接提供服务。  
  
-   “集合大小限制”可限制对间接分配内存或限量供应的资源的消耗。  
  
## 传输配额说明  
 本节介绍可用于下列标准 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 传输的传输配额：HTTP\(S\)、TCP\/IP 和命名管道。自定义传输可以公开它们自己的、未包含在此列表中的可配置配额。若要了解自定义传输的配额，请参考自定义传输的文档。  
  
 每个配额设置都有类型、最小值和默认值。配额的最大值由其类型限制。由于计算机的限制，并不总是可以将配额设置为它的最大值。  
  
|名称|类型|最小<br /><br /> value|Default<br /><br /> value|说明|  
|--------|--------|------------------|-----------------------|--------|  
|`ChannelInitializationTimeout`|TimeSpan|1 个计时周期|5 秒|初始读取过程中等待连接发送前导码的最长时间。此数据在进行身份验证前接收。此设置通常要比 `ReceiveTimeout` 配额值小得多。|  
|`CloseTimeout`|TimeSpan|0|一分钟|在传输引发异常之前等待连接关闭的最长时间。|  
|`ConnectionBufferSize`|Integer|1|8 KB|基础传输的传输和接收缓冲区的大小（以字节为单位）。增加缓冲区大小可以在发送较大消息时提高吞吐量。|  
|`IdleTimeout`|TimeSpan|0|二分钟|已入池连接在关闭前可以保持空闲状态的最长时间。<br /><br /> 此设置仅适用于入池连接。|  
|`LeaseTimeout`|TimeSpan|0|五分钟|已入池的活动连接的最长生存期。在指定时间过后，连接会在当前请求得到服务后立即关闭。<br /><br /> 此设置仅适用于入池连接。|  
|`ListenBacklog`|Integer|1|10|在通往该终结点的其他连接被拒绝之前，侦听器可以拥有的尚未得到服务的连接的最大数量。|  
|`MaxBufferPoolSize`|Long|0|512 KB|传输用于形成可重用消息缓冲池的最大内存（以字节为单位）。当池无法提供消息缓冲区时，系统会分配新的缓冲区以供临时使用。<br /><br /> 创建许多通道工厂或侦听器的安装可能会为缓冲池分配大量内存。在这种情况下，减小此缓冲区大小可以极大地降低内存使用率。|  
|`MaxBufferSize`|Integer|1|64KB|用于对数据进行流处理的缓冲区的最大大小（以字节为单位）。如果未设置此传输配额，或传输未使用流，则该配额值与 `MaxReceivedMessageSize` 配额值和 <xref:System.Int32.MaxValue> 中的较小值相同。|  
|`MaxOutboundConnectionsPerEndpoint`|Integer|1|10|可以与特定终结点相关联的传出连接的最大数量。<br /><br /> 此设置仅适用于入池连接。|  
|`MaxOutputDelay`|TimeSpan|0|200 毫秒|在执行发送操作后为在单个操作中批处理其他消息而等待的最长时间。如果基础传输的缓冲区变满，则消息会较早发送。发送其他消息不会重置延迟期。|  
|`MaxPendingAccepts`|Integer|1|1|侦听器可拥有并等待的最大通道接受数。<br /><br /> 在接受完成与新的接受开始之间有一个时间间隔。增加此集合大小可以防止在此时间间隔中连接的客户端被丢弃。|  
|`MaxPendingConnections`|Integer|1|10|侦听器可以拥有的正在等待应用程序接受的最大连接数。超出此配额值时，新的传入连接会被丢弃而不是等待接受。<br /><br /> 连接功能（如消息安全）可能会使客户端打开多个连接。在设置此配额值时，服务管理员应该考虑这些额外的连接。|  
|`MaxReceivedMessageSize`|Long|1|64KB|所接收消息（包括消息头）的最大大小（以字节为单位）；超出此大小，传输将引发异常。|  
|`OpenTimeout`|TimeSpan|0|一分钟|在传输引发异常之前等待连接建立的最长时间。|  
|`ReceiveTimeout`|TimeSpan|0|十分钟|在传输引发异常之前等待读取操作完成的最长时间。|  
|`SendTimeout`|Timespan|0|一分钟|在传输引发异常之前等待写入操作完成的最长时间。|  
  
 在通过绑定或配置进行设置时，传输配额 `MaxPendingConnections` 和 `MaxOutboundConnectionsPerEndpoint` 被组合为单个传输配额，称为 `MaxConnections`。只有使用绑定元素才能分别设置这些配额值。`MaxConnections` 传输配额具有相同的最小值和默认值。  
  
## 设置传输配额  
 传输配额通过传输绑定元素、传输绑定、应用程序配置或宿主策略进行设置。本文档不涉及通过宿主策略设置传输的内容。若要了解宿主策略配额的设置，请参考基础传输的文档。[配置 HTTP 和 HTTPS](../../../../docs/framework/wcf/feature-details/configuring-http-and-https.md) 主题描述了 Http.sys 驱动程序的配额设置。有关对 HTTP、TCP\/IP 和命名管道连接配置 Windows 限制的更多信息，请参见 Microsoft 知识库。  
  
 其他类型的配额间接应用于传输。传输用来将消息转换为字节的消息编码器可以具有它自己的配额设置。但是，这些配额独立于所使用的传输类型。  
  
### 通过绑定元素控制传输配额  
 通过绑定元素设置传输配额为控制传输行为提供了最大的灵活性。生成通道时，将从绑定中获取关闭、打开、接收和发送操作的默认超时值。  
  
|名称|HTTP|TCP\/IP|命名管道|  
|--------|----------|-------------|----------|  
|`ChannelInitializationTimeout`||X|X|  
|`CloseTimeout`||||  
|`ConnectionBufferSize`||X|X|  
|`IdleTimeout`||X|X|  
|`LeaseTimeout`||X||  
|`ListenBacklog`||X||  
|`MaxBufferPoolSize`|X|X|X|  
|`MaxBufferSize`|X|X|X|  
|`MaxOutboundConnectionsPerEndpoint`||X|X|  
|`MaxOutputDelay`||X|X|  
|`MaxPendingAccepts`||X|X|  
|`MaxPendingConnections`||X|X|  
|`MaxReceivedMessageSize`|X|X|X|  
|`OpenTimeout`||||  
|`ReceiveTimeout`||||  
|`SendTimeout`||||  
  
### 通过绑定控制传输配额  
 通过绑定设置传输配额可提供一组简化的配额以供选择，同时仍然提供对最常用配额值的访问。  
  
|名称|HTTP|TCP\/IP|命名管道|  
|--------|----------|-------------|----------|  
|`ChannelInitializationTimeout`||||  
|`CloseTimeout`|X|X|X|  
|`ConnectionBufferSize`||||  
|`IdleTimeout`||||  
|`LeaseTimeout`||||  
|`ListenBacklog`||X||  
|`MaxBufferPoolSize`|X|X|X|  
|`MaxBufferSize`|1|X|X|  
|`MaxOutboundConnectionsPerEndpoint`||2|2|  
|`MaxOutputDelay`||||  
|`MaxPendingAccepts`||||  
|`MaxPendingConnections`||2|2|  
|`MaxReceivedMessageSize`|X|X|X|  
|`OpenTimeout`|X|X|X|  
|`ReceiveTimeout`|X|X|X|  
|`SendTimeout`|X|X|X|  
  
1.  `MaxBufferSize` 传输配额仅在 `BasicHttp` 绑定上可用。`WSHttp` 绑定适用于不支持流式传输模式的情况。  
  
2.  传输配额 `MaxPendingConnections` 和 `MaxOutboundConnectionsPerEndpoint` 被组合为单个传输配额，称为 `MaxConnections`。  
  
### 通过配置控制传输配额  
 应用程序配置可以设置与直接访问绑定上的属性一样的传输配额。在配置文件中，传输配额的名称总是以小写字母开头。例如，绑定上的 `CloseTimeout` 属性对应于配置中的 `closeTimeout` 设置，而绑定上的 `MaxConnections` 属性对应于配置中的 `maxConnections` 设置。  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>   
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>   
 <xref:System.ServiceModel.Channels.TcpTransportBindingElement>   
 <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>   
 <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>   
 <xref:System.ServiceModel.Channels.TransportBindingElement>