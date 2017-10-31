---
title: "安全会话的安全注意事项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0d5be591-9a7b-4a6f-a906-95d3abafe8db
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# 安全会话的安全注意事项
您应考虑实现安全会话时影响安全的下列事项。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 安全注意事项，请参见 [安全注意事项](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md) 和 [安全性的最佳做法](../../../../docs/framework/wcf/feature-details/best-practices-for-security-in-wcf.md)。  
  
## 安全会话和元数据  
 当建立安全会话并且 <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters.RequireCancellation%2A> 属性设置为 `false` 时，作为服务终结点的 Web Services 描述语言 \(WSDL\) 文档中元数据的一部分，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 发送 `mssp:MustNotSendCancel` 断言。`mssp:MustNotSendCancel` 断言通知客户端此服务不响应取消安全会话的请求。当 <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters.RequireCancellation%2A> 属性设置为 `true` 时，在 WSDL 文档中，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不发出 `mssp:MustNotSendCancel` 断言。当客户端不再需要安全会话时，客户端应向服务发送一个取消请求。当使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 生成客户端时，客户端代码对 `mssp:MustNotSendCancel` 断言的存在与否会做出适当的响应。  
  
## 安全对话和自定义令牌  
 将自定义令牌和派生密钥混合使用会产生一些问题，这是它在 WS\-SecureConversation 规范中的定义方式所导致的。该规范指出 `wsse:SecurityTokenReference` 是引用派生令牌的可选元素：“`/wsc:DerivedKeyToken/wsse:SecurityTokenReference` 此可选元素用来指定安全上下文令牌、安全令牌或用于派生的共享密钥\/机密。如果未指定，则假定收件人可以从消息上下文确定共享密钥。如果无法确定上下文，则应该引发诸如 `wsc:UnknownDerivationSource` 之类的错误。”  
  
 这意味着，如果希望派生自定义令牌，应该将其子句类型包装在 `SecurityTokenReference` 元素中。有一个选项可关闭派生，但是默认为派生密钥。如果无法封装密钥，则对派生密钥令牌进行序列化将成功，但是尝试对其进行反序列化将引发异常。  
  
## 请参阅  
 [如何：在 WSFederationHttpBinding 上禁用安全会话](../../../../docs/framework/wcf/feature-details/how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)   
 [安全注意事项](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)   
 [安全性的最佳做法](../../../../docs/framework/wcf/feature-details/best-practices-for-security-in-wcf.md)