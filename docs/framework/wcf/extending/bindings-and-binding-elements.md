---
title: "绑定和绑定元素 | Microsoft Docs"
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
  - "绑定元素 [WCF]"
ms.assetid: 765ff77b-7682-4ea3-90eb-e4d751e37379
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 绑定和绑定元素
绑定是特殊配置元素（称作“绑定元素”）的集合，服务运行库在每次构造客户端或服务终结点时都对这些元素进行评估。绑定内绑定元素的类型和顺序确定了终结点的通道堆栈中协议和传输通道的选择和堆叠顺序。  
  
 绑定（尤其是系统提供的绑定）通常还具有很多配置属性，这些属性反映了已封装绑定元素的最经常修改的属性。  
  
 绑定必须恰好包含一个传输协议绑定元素。每个传输协议绑定元素都隐含一个默认的消息编码绑定元素，该元素可以通过向绑定中最多添加一个消息编码绑定元素进行重写。除了传输协议和编码器绑定元素以外，绑定还可能包含任意数量的协议绑定元素，这些元素共同实现从一个终结点向其他终结点提供和发送 SOAP 消息所需的功能。有关详细信息，请参见[使用绑定配置服务和客户端](../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)。  
  
## 扩展绑定和绑定元素  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 包含系统提供的绑定，这些绑定涵盖了种类繁多的方案。（有关更多信息，请参见[系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)。）但是，您有时可能需要创建和使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中未包含的绑定。下面的方案需要创建新绑定。  
  
-   若要使用新的绑定元素（例如，新的传输协议、编码或协议绑定元素），您必须创建一个包含该绑定元素的新绑定。例如，如果您为 UDP 传输协议添加了一个自定义 `UdpTransportBindingElement`，则需要创建一个新绑定来利用它。有关使用 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName> 类型完成此行为的信息，请参见[自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md)。  
  
-   以系统提供的绑定没有在公共属性上公开的方式配置现有绑定元素。例如，必须创建一个新绑定以更改签名和加密操作的执行顺序。有关完成此行为的信息，请参见[如何：自定义系统提供的绑定](../../../../docs/framework/wcf/extending/how-to-customize-a-system-provided-binding.md)。  
  
-   建立仅公开特定配置选项的公司标准绑定。例如，若要为您的公司创建不能禁用安全的 <xref:System.ServiceModel.WSHttpBinding> 变体，可以创建一个行为方式类似于 <xref:System.ServiceModel.WSHttpBinding> 但总是启用安全的新绑定。有关详细信息，请参见[创建用户定义的绑定](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md)。  
  
-   若要执行某种元数据自定义，通常可以配置或使用某个自定义绑定元素，但并非必须这样做。有关向绑定和绑定元素提供元数据支持的更多信息，请参见[配置和元数据支持](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md)。  
  
-  
  
## 通道、绑定和绑定元素  
 绑定和绑定元素是应用程序编程模型（包括属性和行为）与通道模型（包括工厂和侦听器、消息编码器以及传输协议和协议实现）之间的联系。通常，实现绑定元素和绑定的目的是使通道能够被应用程序层使用。  
  
 通道层向服务层发送消息或从服务层接收消息，并且在终结点之间传输这些消息。在客户端上，通道层是一个通道工厂堆栈，这些通道工厂创建通向网络终结点的通道。在服务上，通道层是一个通道侦听器堆栈，这些侦听器接受在网络终结点收到的通道。  
  
 有两种常规类型的通道：协议通道和传输通道。传输通道负责在网络终结点之间实际传输消息。传输通道必须具有默认消息编码器，并且应该能够使用通过消息编码器绑定元素提供的备用消息编码器。消息编码器负责将 <xref:System.ServiceModel.Channels.Message?displayProperty=fullName> 转换为网络表示以及执行反向转换。协议通道负责实现 SOAP 级协议（例如，WS\-Security 或 WS\-ReliableMessaging）。  
  
 传输通道和协议通道的主要要求是它们需要实现必需的通道接口。若要创建有效的通道层，它们必须具有关联的工厂和侦听器，等等。若要使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的通道实现，对于每个通道，都需要有一个派生自 <xref:System.ServiceModel.Channels.BindingElement> 的关联绑定元素，并且应该有一个派生自 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> 的相关绑定扩展元素，以便包括到配置文件中。  
  
 如前所述，可以将消息编码器、协议和传输通道实现的绑定元素堆叠起来，以形成一个通道堆栈，而用来将它们组织成一个有序集的机制就是绑定。绑定和绑定元素将应用程序编程模型与通道模型联系起来。您可以在代码中直接使用自己的通道实现，但是除非将编码器、传输和协议实现为绑定元素，否则无法在服务层编程模型中使用它们。  
  
 有关开发通道及其绑定元素的详细信息，请参见[扩展通道层](../../../../docs/framework/wcf/extending/extending-the-channel-layer.md)。