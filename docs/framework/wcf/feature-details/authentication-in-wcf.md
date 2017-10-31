---
title: "WCF 中的身份验证 | Microsoft Docs"
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
  - "身份验证 [WCF]"
  - "安全性 [WCF], Authentication — 身份验证"
ms.assetid: 9254d873-843d-4c6e-bea4-8184ac3e44f4
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# WCF 中的身份验证
下面的主题演示 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中用于提供身份验证的多个不同机制，例如 Windows 身份验证、X.509 证书以及用户名和密码。  
  
## 本节内容  
 [如何：使用 ASP.NET 成员资格提供程序](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)  
 ASP.NET 功能包括成员资格和角色提供程序、用于存储用户名\/密码对以供进行身份验证的数据库，以及用于身份验证的用户角色。本主题说明 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务如何使用同一数据库对用户进行身份验证和授权。  
  
 [如何：使用自定义用户名和密码验证程序](../../../../docs/framework/wcf/feature-details/how-to-use-a-custom-user-name-and-password-validator.md)  
 演示如何集成自定义用户名\/密码验证程序。  
  
 [服务标识和身份验证](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)  
 客户端可以通过指定期望的服务标识对服务进行身份验证，这是一种额外的保护措施。如果期望的标识与服务返回的标识不匹配，则身份验证失败。  
  
 [安全协商和超时](../../../../docs/framework/wcf/feature-details/security-negotiation-and-timeouts.md)  
 说明如何使用 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings> 类的 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.NegotiationTimeout%2A> 属性。  
  
 [调试 Windows 身份验证错误](../../../../docs/framework/wcf/feature-details/debugging-windows-authentication-errors.md)  
 重点说明使用 Windows 身份验证时所遇到的常见问题。  
  
## 参考  
 <xref:System.ServiceModel>  
  
## 相关章节  
 [常用安全方案](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md)  
  
## 请参阅  
 [安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Windows Server App Fabric 的安全模型](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x804)