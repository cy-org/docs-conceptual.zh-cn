---
title: "自定义令牌 | Microsoft Docs"
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
  - "安全 [WCF], 自定义令牌"
ms.assetid: 8b2dbe29-dec2-4652-8e34-fb21bc1437b5
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 自定义令牌
虽然 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 以本机方式支持将 X.509 证书、安全上下文令牌、Kerberos 票证和用户名令牌作为凭据，但是它的灵活程度足以使您使用自己的自定义凭据。  
  
## 本节内容  
 [如何：创建自定义令牌](../../../../docs/framework/wcf/extending/how-to-create-a-custom-token.md)  
 描述如何使用 <xref:System.IdentityModel.Tokens.SecurityToken> 类创建自定义安全令牌，以及如何将其与自定义安全令牌提供程序和身份验证器进行集成。