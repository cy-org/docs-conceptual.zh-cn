---
title: "&lt;标识&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1d2ae56-e231-4a07-9c3f-9f13381dc0d8
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# &lt;标识&gt;
标识元素允许客户端开发人员在设计时指定服务的期望标识。  在客户端与服务之间的握手过程中，[!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 基础结构将确保预期服务的标识与此元素的值相匹配，从而可以进行身份验证。  有关详细信息，请参阅[服务标识和身份验证](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)。  
  
## 语法  
  
```  
  
<identity>  
    <certificate encodedValue="String"/>  
    <certificateReference findValue="String"   
       isChainIncluded="Boolean"  
       storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"storeName="  
       storeLocation="LocalMachine/CurrentUser"  
       X509FindType= Enumeration./>  
    <dns value="String"/>  
    <rsa value="String"/>  
    <servicePrincipalName value="String"/>  
    <usePrincipalName value="String"/>  
</identity>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|certificate|指定 X.509 证书的设置。  此元素的类型为 <xref:System.ServiceModel.Configuration.CertificateElement>。  它包含一个 `encodedValue` 属性，该属性是一个字符串，用于指定此证书编码的值。|  
|certificateReference|指定 X.509 证书验证的设置。  此元素的类型为 <xref:System.ServiceModel.Configuration.CertificateReferenceElement>。|  
|dns|指定用于对服务进行身份验证的 X.509 证书的 DNS。  此元素包含一个字符串属性 `value`，并包含实际的标识。|  
|rsa|指定用于向客户端验证服务身份的 X.509 证书的 RSA 字段的值。  此元素包含一个字符串属性 `value`，并包含实际的标识。|  
|servicePrincipalName|指定服务器主体名称 \(SPN\) 标识，它是客户端用来唯一标识一个服务实例的主体名称。  此元素包含一个 `value` 属性，该属性是一个字符串，其中包含实际的主体名称。  此元素的类型为 <xref:System.ServiceModel.Configuration.ServicePrincipalNameElement>。|  
|userPrincipalName|指定用户主体名称 \(UPN\) 标识，它是网络上的用户登录名类型。  用户主体名称包含 Active Directory 中使用的用户对象名称，后跟一个 @ 符号并且通常随后紧跟域名系统的父域。  例如，Fabrikam.com 域树中的 Jeff 可能具有用户主要名称 [jeff@fabrikam.com](mailto:jeffsmith@fabrikam.com)。  此元素包含一个 `value` 属性，该属性是一个字符串，其中包含实际的主体名称。  此元素的类型为 <xref:System.ServiceModel.Configuration.UserPrincipalNameElement>。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<自定义\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custom.md)|指定 netPeerTcpBinding 的自定义对等解析程序。|  
|[\<endpoint\>](http://msdn.microsoft.com/zh-cn/13aa23b7-2f08-4add-8dbf-a99f8127c017)|配置不同类型的终结点。|  
|[\<issuer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuer.md)|指定联合服务的安全令牌服务 \(STS\)。|  
|[\<issuerMetadata\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuermetadata.md)|指定联合服务的安全令牌服务 \(STS\) 的元数据终结点。|  
|[\<issuedTokenParameters\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenparameters.md)|定义自定义绑定中的已颁发令牌的参数。|  
|[\<localIssuer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/localissuer.md)|指定本地安全令牌服务 \(STS\)。|  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.IdentityElement>   
 <xref:System.ServiceModel.EndpointAddress>   
 <xref:System.ServiceModel.EndpointAddress.Identity%2A>   
 [服务标识和身份验证](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)   
 [终结点：地址、绑定和协定](../../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)