---
title: "扩展 WCF | Microsoft Docs"
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
  - "扩展性 [WCF]"
  - "WCF, 扩展性"
  - "Windows Communication Foundation, 扩展性"
ms.assetid: c145e2f6-f402-41f5-8b5a-eee03978737b
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# 扩展 WCF
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 使您能够修改和扩展运行时组件，以便精确控制和扩展基于服务的应用程序。  本节中的主题深入探讨了有关扩展性体系结构的内容。  有关基础编程的更多信息，请参见[基本 WCF 编程](../../../../docs/framework/wcf/basic-wcf-programming.md)。  
  
## 本节内容  
 [扩展 ServiceHost 和服务模块层](../../../../docs/framework/wcf/extending/extending-servicehost-and-the-service-model-layer.md)  
 服务模型层负责从基础通道提取出传入的消息，将它们翻译成应用程序代码形式的方法调用，并将结果发送回调用方。  服务模型扩展将修改或实现执行或通信行为，功能包括调度程序功能、自定义行为、消息和参数侦听以及其他扩展性功能。  
  
 [扩展绑定](../../../../docs/framework/wcf/extending/extending-bindings.md)  
 绑定是描述连接到终结点所需的通信详细信息的对象。  绑定扩展或自定义绑定实现了支持应用程序功能所需的自定义通信功能。  
  
 [扩展通道层](../../../../docs/framework/wcf/extending/extending-the-channel-layer.md)  
 通道层位于服务模型层的下方并且负责客户端和服务之间的消息交换。  通道扩展可以实现新的协议功能，例如安全性。  通道扩展也可以传输功能，例如实现新的网络传输以传送 SOAP 消息。  
  
 [扩展安全性](../../../../docs/framework/wcf/extending/extending-security.md)  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的安全性由传输安全（完整性、保密性和身份验证）、访问控制（授权）和审核组成。  在 `IdentityModel` 命名空间中找到的类由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 用于访问控制。  了解安全体系结构使您可以创建自定义声明类型，以便容纳自定义访问控制系统。  
  
 [扩展元数据系统](../../../../docs/framework/wcf/extending/extending-the-metadata-system.md)  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 元数据系统由一组类和接口组成，这些表示元数据的类和接口是实现基于服务的应用程序所必需的。  修改或扩展这些类，或者实现和配置这些接口，以便导出和导入自定义元数据（如 Web 服务描述语言 \(WSDL\) 扩展或自定义的 WS\-PolicyAttachments 断言）。  
  
 [扩展编码器和序列化程序](../../../../docs/framework/wcf/extending/extending-encoders-and-serializers.md)  
 编码器和序列化程序将数据从一种形式转换成另一种形式。  本节中的主题讨论如何扩展已提供的类以满足特殊要求。  
  
## 参考  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
 <xref:System.ServiceModel.Description>  
  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.IdentityModel.Policy>  
  
 <xref:System.IdentityModel.Selectors>  
  
 <xref:System.IdentityModel.Tokens>  
  
## 相关章节  
 [基本 WCF 编程](../../../../docs/framework/wcf/basic-wcf-programming.md)  
  
 [WCF 功能详细信息](../../../../docs/framework/wcf/feature-details/index.md)  
  
 [准则与最佳做法](../../../../docs/framework/wcf/guidelines-and-best-practices.md)