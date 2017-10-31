---
title: "SAML 令牌和声明 | Microsoft Docs"
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
  - "联合"
  - "颁发的令牌"
  - "SAML 令牌"
  - "WCF, 联合"
ms.assetid: 930b6e34-9eab-4e95-826c-4e06659bb977
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# SAML 令牌和声明
安全断言标记语言 \(SAML\) 令牌是声明的 XML 表示形式。默认情况下，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 在联合安全方案中使用的 SAML 令牌称作“已颁发令牌”。  
  
 SAML 令牌包含由一个实体所生成的关于另一实体的多组声明的语句。例如，在联合安全方案中，语句是由安全令牌服务针对系统中的某一用户所生成的。安全令牌服务将对 SAML 令牌进行签名，以指示令牌中所包含语句的真实性。此外，SAML 令牌与 SAML 令牌用户确实了解的加密密钥材料关联。这就向依赖方证明了 SAML 令牌实际上是颁发给该用户的。例如，在典型的方案中：  
  
1.  客户端向安全令牌服务请求 SAML 令牌，并通过使用 Windows 证书对该安全令牌服务进行身份验证。  
  
2.  安全令牌服务向客户端颁发 SAML 令牌。SAML 令牌使用与安全令牌服务关联的证书进行签名，并包含针对目标服务所加密的校验密钥。  
  
3.  客户端还将接收校验密钥的副本，然后将 SAML 令牌提交到应用程序服务（依赖方）并使用该校验密钥对消息进行签名。  
  
4.  依赖方可通过 SAML 令牌上的签名了解到，该令牌是由安全令牌服务颁发的；依赖方还可通过使用校验密钥创建的消息签名了解到，该令牌是颁发给客户端的。  
  
## 从 Claim 到 SamlAttribute  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，SAML 令牌中的语句是作为 <xref:System.IdentityModel.Tokens.SamlAttribute> 对象建模的，可以直接从 <xref:System.IdentityModel.Claims.Claim> 对象填充，前提是 <xref:System.IdentityModel.Claims.Claim> 对象的 <xref:System.IdentityModel.Claims.Claim.Right%2A> 属性为 <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>，并且 <xref:System.IdentityModel.Claims.Claim.Resource%2A> 属性的类型为 <xref:System.String>。例如：  
  
 [!code-csharp[c_CreateSTS#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#8)]
 [!code-vb[c_CreateSTS#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#8)]  
  
> [!NOTE]
>  如果 SAML 令牌在消息中序列化，无论是在安全令牌服务颁发这些令牌时，还是在客户端将其作为身份验证的一部分提交到服务中时，最大消息大小配额都必须足够大，以便能够容纳 SAML 令牌和其他消息部分。正常情况下，默认消息大小配额足够使用。但是，如果 SAML 令牌由于包含数以百计的声明而过于庞大，您可能需要提高配额，以便容纳序列化的令牌。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][数据的安全考虑事项](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md).  
  
## 从 SamlAttribute 到 Claim  
 在消息中接收到 SAML 令牌时，SAML 令牌中的各种语句将转换为 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 对象，并放置在 <xref:System.IdentityModel.Policy.AuthorizationContext> 中。来自每个 SAML 语句的声明将由 <xref:System.IdentityModel.Policy.AuthorizationContext> 的 <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> 属性返回，并可对这些声明进行检查，以确定是否对该用户进行身份验证和授权。  
  
## 请参阅  
 <xref:System.IdentityModel.Policy.AuthorizationContext>   
 <xref:System.IdentityModel.Policy.IAuthorizationPolicy>   
 <xref:System.IdentityModel.Claims.ClaimSet>   
 [联合](../../../../docs/framework/wcf/feature-details/federation.md)   
 [如何：创建联合客户端](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [如何：在联合身份验证服务上配置凭据](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)   
 [使用标识模型管理声明和授权](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)   
 [声明和令牌](../../../../docs/framework/wcf/feature-details/claims-and-tokens.md)   
 [声明创建和资源值](../../../../docs/framework/wcf/feature-details/claim-creation-and-resource-values.md)   
 [如何：创建自定义声明](../../../../docs/framework/wcf/extending/how-to-create-a-custom-claim.md)