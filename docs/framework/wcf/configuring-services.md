---
title: "正在配置服务 | Microsoft Docs"
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
  - "配置 [WCF]"
ms.assetid: beac771e-f28e-4f84-9ff1-ad9251c726d3
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# 正在配置服务
在设计和实现服务协定后，即可配置服务。  在其中可以定义和自定义如何向客户端公开服务，包括指定可以找到服务的地址、服务用于发送和接收消息的传输和消息编码，以及服务需要的安全类型。  
  
 此处使用的配置包括在代码中以强制方式或通过使用配置文件定义和自定义服务的各个方面的所有方法，例如指定其终结点地址、使用的传输及其安全方案。  实际上，编写配置是 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 应用程序编程的主要部分。  
  
## 本节内容  
 [简化配置](../../../docs/framework/wcf/simplified-configuration.md)  
 从 [!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)] 开始，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 附带一个新的默认配置模型，该模型简化了 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 配置要求。  如果您没有为特定服务提供任何 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 配置，运行时将自动使用默认终结点、绑定和行为配置您的服务。  
  
 [使用配置文件配置服务](../../../docs/framework/wcf/configuring-services-using-configuration-files.md)  
 可使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 配置技术对 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务进行配置。  通常情况下，向承载 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务的 Internet 信息服务 \(IIS\) 网站的 Web.config 文件添加 XML 元素。  这些元素允许您更改详细信息，例如每台计算机上的终结点地址（用于与服务进行通信的实际地址）。  
  
 [绑定](../../../docs/framework/wcf/bindings.md)  
 此外，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 包括几个绑定形式的系统提供的常见配置，这些绑定使您可以快速为客户端和服务的通信方式选择最基本的功能，例如所使用的传输、安全性和消息编码。  
  
 [终结点](../../../docs/framework/wcf/endpoints.md)  
 与 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务的所有通信是通过该服务的终结点进行的。  终结点包含协定、在绑定中指定的配置信息，以及指示查找服务或获取该服务相关信息的位置的地址。  
  
 [保证服务的安全](../../../docs/framework/wcf/securing-services.md)  
 使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 和现有安全机制，可以将保密性、完整性、身份验证和授权实现到任何服务中。  还可以审核安全成功和安全失败。  
  
 [创建 WS\-I 基本配置文件 1.1 可互操作服务](../../../docs/framework/wcf/creating-ws-i-basic-profile-1-1-interoperable-services.md)  
 WS\-I 基本配置文件 1.1 规范中概述了部署服务的要求，该服务可与其他任何平台或操作系统上的服务和客户端进行互操作。  
  
## 参考  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
 <xref:System.ServiceModel.Description>  
  
## 相关章节  
 [基本编程生命周期](../../../docs/framework/wcf/basic-programming-lifecycle.md)  
  
 [设计和实现服务](../../../docs/framework/wcf/designing-and-implementing-services.md)  
  
 [承载服务](../../../docs/framework/wcf/hosting-services.md)  
  
 [生成客户端](../../../docs/framework/wcf/building-clients.md)  
  
 [扩展性介绍](../../../docs/framework/wcf/introduction-to-extensibility.md)  
  
 [管理和诊断](../../../docs/framework/wcf/diagnostics/index.md)  
  
## 请参阅  
 [基本 WCF 编程](../../../docs/framework/wcf/basic-wcf-programming.md)   
 [概念概述](../../../docs/framework/wcf/conceptual-overview.md)   
 [WCF 功能详细信息](../../../docs/framework/wcf/feature-details/index.md)