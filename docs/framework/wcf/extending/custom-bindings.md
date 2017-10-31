---
title: "自定义绑定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "Windows Communication Foundation, 配置"
  - "Windows Communication Foundation, 终结点"
ms.assetid: 58532b6d-4eea-4a4f-854f-a1c8c842564d
caps.latest.revision: 33
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 33
---
# 自定义绑定
当系统提供的某个绑定不符合服务的要求时，可使用 <xref:System.ServiceModel.Channels.CustomBinding> 类。所有绑定都是从绑定元素的有序集构造而来的。自定义绑定可以从一组系统提供的绑定元素生成，也可以包含用户定义的自定义绑定元素。例如，可以使用自定义绑定元素在服务终结点处使用新的传输或编码器。有关可运行示例，请参见[Custom Binding Samples](http://msdn.microsoft.com/zh-cn/657e8143-beb0-472d-9cfe-ed1a19c2ab08)。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md).  
  
## 自定义绑定的构造  
 自定义绑定是使用 <xref:System.ServiceModel.Channels.CustomBinding.%23ctor%2A> 构造函数并通过“堆叠”在一起的绑定元素的集合构造的，这些元素的特定顺序如下：  
  
-   最顶层是一个允许流事务的可选 <xref:System.ServiceModel.Channels.TransactionFlowBindingElement> 类。  
  
-   接下来是一个可选的 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> 类，它提供了 WS\-ReliableMessaging 规范中定义的会话和排序机制。会话可通过 SOAP 和传输中介。  
  
-   接下来是一个可选的 <xref:System.ServiceModel.Channels.SecurityBindingElement> 类，它提供了授权、身份验证、保护和机密性等安全功能。  
  
-   接下来是一个可选的 <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement> 类，它提供了通过本身不支持双工通信的传输协议（例如 HTTP）进行双向双工通信的功能。  
  
-   接下来是一个可选的 <xref:System.ServiceModel.Channels.OneWayBindingElement> 类，它提供了单向通信。  
  
-   接下来是一个可选的流安全绑定元素，它可以是以下元素之一。  
  
    -   <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>  
  
-   接下来是一个必需的消息编码绑定元素。可以使用自己的消息编码器或者以下三种消息编码绑定之一：  
  
    -   <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>  
  
 底层是一个必需的传输元素。可以使用自己的传输，或者使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 提供的以下传输绑定元素之一：  
  
-   <xref:System.ServiceModel.Channels.TcpTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.HttpTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.PeerTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>  
  
-   <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBindingElement>  
  
-   <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>  
  
 下表总结了每层的选项。  
  
|层|选项|必需|  
|-------|--------|--------|  
|事务|<xref:System.ServiceModel.Channels.TransactionFlowBindingElement>|否|  
|可靠性|<xref:System.ServiceModel.Channels.ReliableSessionBindingElement>|否|  
|安全性|<xref:System.ServiceModel.Channels.SecurityBindingElement>|否|  
|编码|文本、二进制、消息传输优化机制 \(MTOM\)、自定义|是|  
|传输|TCP、HTTP、HTTPS、命名管道（也称为 IPC）、对等 \(P2P\)、消息队列（也称为 MSMQ）、自定义|是|  
  
 此外，可以定义自己的绑定元素，并将它们插在前面定义的任何层之间。  
  
## 请参阅  
 [终结点创建概述](../../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [使用绑定配置服务和客户端](../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)   
 [如何：自定义系统提供的绑定](../../../../docs/framework/wcf/extending/how-to-customize-a-system-provided-binding.md)   
 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [自定义绑定](../../../../docs/framework/wcf/samples/custom-binding.md)