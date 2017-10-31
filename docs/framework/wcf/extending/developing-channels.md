---
title: "开发通道 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0513af9f-a0c2-457b-9a50-5b6bfee48513
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 开发通道
开发可以与 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 应用程序层一起使用的协议或传输通道需要多个步骤。本主题介绍这些步骤并为您指出特定主题以了解更多信息。若要了解本主题中提及的通道模型和各种类型，请参见[通道模型概述](../../../../docs/framework/wcf/extending/channel-model-overview.md)。有关完整的传输通道示例，请参见[传输：UDP](../../../../docs/framework/wcf/samples/transport-udp.md)。  
  
## 通道开发任务列表  
 创建用户定义的通道的步骤如下所示：所有通道必须：  
  
1.  确定您的 <xref:System.ServiceModel.Channels.IChannelFactory> 和 <xref:System.ServiceModel.Channels.IChannelListener> 将支持哪种通道消息交换模式（<xref:System.ServiceModel.Channels.IOutputChannel>、<xref:System.ServiceModel.Channels.IInputChannel>、<xref:System.ServiceModel.Channels.IDuplexChannel>、<xref:System.ServiceModel.Channels.IRequestChannel> 或 <xref:System.ServiceModel.Channels.IReplyChannel>），以及该模式是否支持这些接口的会话变体。有关详细信息，请参见[选择消息交换模式](../../../../docs/framework/wcf/extending/choosing-a-message-exchange-pattern.md)。  
  
2.  创建支持您的消息交换模式的通道工厂和侦听器（<xref:System.ServiceModel.Channels.IChannelFactory> 和 <xref:System.ServiceModel.Channels.IChannelListener>）。有关开发工厂的详细信息，请参见[客户端：通道工厂和通道](../../../../docs/framework/wcf/extending/client-channel-factories-and-channels.md)。有关开发侦听器的详细信息，请参见[服务：通道侦听器和通道](../../../../docs/framework/wcf/extending/service-channel-listeners-and-channels.md)。  
  
3.  确保将任何特定于网络的异常规范化为 <xref:System.TimeoutException?displayProperty=fullName> 或 <xref:System.ServiceModel.CommunicationException> 的相应派生类。有关详细信息，请参见[处理异常和错误](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md)。  
  
4.  若要从应用程序层使用通道，请添加一个可将自定义通道添加到通道堆栈的 <xref:System.ServiceModel.Channels.BindingElement>。有关更多信息，请参见[创建 BindingElement](../../../../docs/framework/wcf/extending/creating-a-bindingelement.md)。  
  
 要在应用程序层启用更完全的支持，需要执行以下附加步骤：  
  
1.  添加一个绑定元素扩展部分，用于向配置系统公开新的绑定元素。有关更多信息，请参见[配置和元数据支持](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md)。  
  
2.  添加元数据扩展以将各种功能传递给其他终结点。有关更多信息，请参见[配置和元数据支持](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md)。  
  
3.  添加一个绑定，以根据准确定义的配置文件预先配置绑定元素堆栈。有关更多信息，请参见[创建用户定义的绑定](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md)。  
  
4.  添加一个绑定部分和绑定配置元素，用于向配置系统公开该绑定。有关更多信息，请参见[配置和元数据支持](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md)。  
  
## 请参阅  
 [扩展绑定](../../../../docs/framework/wcf/extending/extending-bindings.md)