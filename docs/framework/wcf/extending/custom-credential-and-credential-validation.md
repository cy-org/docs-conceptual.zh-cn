---
title: "自定义凭据和凭据验证 | Microsoft Docs"
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
  - "凭据验证 [WCF]"
  - "凭据 [WCF]"
  - "凭据 [WCF], 自定义"
  - "凭据 [WCF], 验证"
  - "自定义凭据 [WCF]"
ms.assetid: da831bec-e281-4d44-b343-437b5eef688e
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 自定义凭据和凭据验证
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的安全性基于服务与客户端之间的凭据交换。  大多数安全方案均可使用常见的凭据类型来实现，如 Windows \(Kerberos\)、用户名和密码以及证书。  而本节中的主题针对需要使用新类型的凭据的情况说明如何处理和验证这些新类型。  
  
## 本节内容  
 [如何：创建使用自定义证书验证程序的服务](../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)  
 介绍如何通过从 <xref:System.IdentityModel.Selectors.X509CertificateValidator> 类继承来自定义 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 验证。  
  
 [演练：创建自定义客户端和服务凭据](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md)  
 演示如何扩展 <xref:System.ServiceModel.Description.ClientCredentials> 和 <xref:System.ServiceModel.Description.ServiceCredentials> 类以容纳新的凭据类型。  这是介绍如何创建自定义凭据类型的系列主题中的第一个主题。  
  
 [如何：创建自定义安全令牌提供程序](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-provider.md)  
 说明如何创建安全令牌提供程序来处理新的凭据类型并返回凭据的新令牌。  这是该系列主题中的第二个主题。  
  
 [如何：创建自定义安全令牌身份验证器](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-authenticator.md)  
 说明如何创建自定义身份验证器来验证新的凭据类型。  这是该系列主题中的第三个主题。  
  
## 参考  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.IdentityModel.Policy>  
  
 <xref:System.IdentityModel.Tokens>  
  
 <xref:System.IdentityModel.Selectors>  
  
 <xref:System.IdentityModel.Selectors.X509CertificateValidator>  
  
 <xref:System.ServiceModel.Description.ClientCredentials>  
  
 <xref:System.ServiceModel.Description.ServiceCredentials>  
  
## 相关章节  
 [身份验证](../../../../docs/framework/wcf/feature-details/authentication-in-wcf.md)  
  
 [联合令牌与颁发的令牌](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)  
  
 [授权](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)  
  
## 请参阅  
 [安全性](../../../../docs/framework/wcf/feature-details/security.md)