---
title: "扩展安全性 | Microsoft Docs"
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
  - "安全 [WCF], 扩展"
ms.assetid: a015a040-9fdf-4147-9ea9-f83b570be1d4
caps.latest.revision: 23
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 23
---
# 扩展安全性
若要容纳新的声明类型和自定义令牌，您可以扩展 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 的安全基础结构。本节中的主题将向您介绍如何完成此任务。  
  
## 本节内容  
 [Security Architecture](http://msdn.microsoft.com/zh-cn/16593476-d36a-408d-808c-ae6fd483e28f)  
 浏览 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全系统的体系结构。  
  
 [自定义凭据和凭据验证](../../../../docs/framework/wcf/extending/custom-credential-and-credential-validation.md)  
 说明在验证自定义凭据时如何使用标识模型。  
  
 [自定义令牌](../../../../docs/framework/wcf/extending/custom-tokens.md)  
 安全令牌服务 \(STS\) 颁发的令牌通常为 SAML 令牌。本主题说明如何创建自定义令牌类型。  
  
 [自定义授权](../../../../docs/framework/wcf/extending/custom-authorization.md)  
 说明如何实现自定义授权。  
  
 [重写服务标识以便进行身份验证](../../../../docs/framework/wcf/extending/overriding-the-identity-of-a-service-for-authentication.md)  
 介绍如何重写身份验证服务的标识。  
  
 [如何：创建自定义客户端标识验证工具](../../../../docs/framework/wcf/extending/how-to-create-a-custom-client-identity-verifier.md)  
 演示如何验证自定义终结点标识。  
  
 [如何：使用独立的 X.509 证书进行签名和加密](../../../../docs/framework/wcf/extending/how-to-use-separate-x-509-certificates-for-signing-and-encryption.md)  
 通常使用单个证书对消息进行签名和加密。本主题说明如何按照要求使用两个证书。  
  
 [如何：更改 X.509 证书私钥的加密提供程序](../../../../docs/framework/wcf/extending/change-cryptographic-provider-x509-certificate-private-key.md)  
 说明如何更改用于提供 X.509 证书的私钥的加密提供程序以及如何将该提供程序集成到 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 框架中。  
  
## 参考  
 <xref:System.ServiceModel.ServiceAuthorizationManager>  
  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.IdentityModel.Policy>  
  
 <xref:System.IdentityModel.Tokens>  
  
 <xref:System.IdentityModel.Selectors>  
  
## 相关章节  
 [安全性](../../../../docs/framework/wcf/feature-details/security.md)  
  
 [基本 WCF 编程](../../../../docs/framework/wcf/basic-wcf-programming.md)  
  
## 请参阅  
 [安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)