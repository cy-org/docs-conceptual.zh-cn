---
title: "&lt;issuedTokenParameters&gt; 的 &lt;issuerMetadata&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1a85ca37-496d-4fa3-8d44-d6c9383d735c
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;issuedTokenParameters&gt; 的 &lt;issuerMetadata&gt;
## 语法  
  
```  
  
<issuerMetaData address=String"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|address|必需。  一个指定终结点地址的字符串。  该地址必须为绝对 URI。  默认值为一个空字符串。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<页眉\>](../../../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md)|一个地址标头集合。|  
|[\<标识\>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|一个标识，与某个终结点交换消息的其他终结点可以使用该标识对该终结点进行身份验证。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<issuedTokenParameters\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenparameters.md)|指定在联合安全方案中颁发的安全令牌的参数。|  
  
## 请参阅  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters>   
 <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [服务标识和身份验证](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)   
 [联合令牌与颁发的令牌](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)   
 [使用自定义绑定的安全功能](../../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)   
 [联合令牌与颁发的令牌](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [扩展绑定](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [自定义绑定](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [如何：使用 SecurityBindingElement 创建自定义绑定](../../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)   
 [自定义绑定安全性](../../../../../docs/framework/wcf/samples/custom-binding-security.md)