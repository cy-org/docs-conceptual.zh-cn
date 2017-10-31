---
title: "保护服务和客户端的安全 | Microsoft Docs"
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
  - "消息安全 [WCF]"
ms.assetid: e681f3bd-0c09-4a58-b0e4-0ecbdf1aa6c7
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# 保护服务和客户端的安全
本节中的信息主要针对 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的编程安全。  通常，这包括选择系统提供的相应绑定、设置安全元素的属性，然后设置服务行为的属性（控制检索凭据以供服务或客户端使用的方式）。  这些技术涵盖了大多数用户对大多数方案的安全要求，如[常用安全方案](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md)中所示。  如果您的方案要求更多功能，请首先参见[使用自定义绑定的安全功能](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)；如果解决方案并不一目了然，请参见[扩展安全性](../../../../docs/framework/wcf/extending/extending-security.md)。  如果您要创建使用丰富声明的系统（或与其交互），请参见[授权](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)中的主题。  
  
## 本节内容  
 [WCF 安全编程](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)  
 用于保护消息安全的编程模型概述。  
  
 [传输安全概述](../../../../docs/framework/wcf/feature-details/transport-security-overview.md)  
 如何通过传输层保护消息安全概述。  
  
 [消息安全](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)  
 总结在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中使用消息级安全的原因。  
  
 [安全会话](../../../../docs/framework/wcf/feature-details/secure-sessions.md)  
 讨论保护 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会话的安全时必须考虑的注意事项。  
  
 [使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)  
 说明使用 X.509 证书时必须完成的一些常见任务。  
  
## 参考  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
 <xref:System.ServiceModel.Security>  
  
## 相关章节  
 [安全性概念](../../../../docs/framework/wcf/feature-details/security-concepts.md)  
  
 [扩展安全性](../../../../docs/framework/wcf/extending/extending-security.md)  
  
 [常用安全方案](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md)  
  
 [绑定与安全](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)  
  
 [使用自定义绑定的安全功能](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)  
  
 [扩展安全性](../../../../docs/framework/wcf/extending/extending-security.md)  
  
 [授权](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)  
  
## 请参阅  
 [基本 WCF 编程](../../../../docs/framework/wcf/basic-wcf-programming.md)   
 [Windows Server App Fabric 的安全模型 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)