---
title: "&lt;clientCredentials&gt; 的 &lt;serviceCertificate&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e50c0ac5-f0df-4c90-b54b-fc602c1f84ea
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;clientCredentials&gt; 的 &lt;serviceCertificate&gt; 元素
指定客户端对服务进行身份验证时使用的证书。  
  
## 语法  
  
```  
  
<serviceCertificate />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<defaultCertificate\>](../../../../../docs/framework/configure-apps/file-schema/wcf/defaultcertificate-element.md)|指定在服务或 STS 未通过协商协议提供证书时要使用的 X.509 证书。|  
|[\<scopedCertificates\>](../../../../../docs/framework/configure-apps/file-schema/wcf/scopedcertificates-element.md)|表示特定服务为身份验证提供的 X.509（作用域）证书的集合。  此集合通常用于指定联合方案中安全令牌服务的服务证书。|  
|[\<Authentication — 身份验证\>](../../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md)|指定客户端使用的服务证书的身份验证行为。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<clientCredentials\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|指定客户端用于向服务证明自己的身份的凭据。|  
  
## 备注  
 此配置元素指定客户端在验证使用 SSL 身份验证的服务所出示的证书时使用的设置。  它还包含在客户端上显式配置为对发送给使用消息安全的服务的消息进行加密的服务的所有证书。  
  
 `serviceCertificate` 元素的属性与 [\<clientCertificate\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcertificate-of-clientcredentials-element.md) 的属性相同。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement.ServiceCertificate%2A>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Description.ClientCredentials.ServiceCertificate%2A>   
 <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement>   
 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>   
 [安全行为](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [保证客户端的安全](../../../../../docs/framework/wcf/securing-clients.md)   
 [使用证书](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)