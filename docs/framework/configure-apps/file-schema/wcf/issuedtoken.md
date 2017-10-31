---
title: "&lt;issuedToken&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6eae4b7-a6cd-4e1a-b0f6-f407022550b0
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;issuedToken&gt;
指定用于向服务验证客户端身份的自定义令牌。  
  
## 语法  
  
```  
  
<issuedToken   
   cacheIssuedTokens="Boolean"  
   defaultKeyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"  
   issuedTokenRenewalThresholdPercentage = "0 to 100"  
   issuerChannelBehaviors="String"  
      localIssuerChannelBehaviors="String"  
   maxIssuedTokenCachingTime="TimeSpan"  
</issuedToken>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`cacheIssuedTokens`|可选的布尔值属性，指定是否对令牌进行缓存。  默认值为 `true`。|  
|`defaultKeyEntropyMode`|可选的字符串属性，指定用于握手操作的随机值（熵）。  这些值包括 `ClientEntropy`、`ServerEntropy` 和 `CombinedEntropy`，默认值为 `CombinedEntropy`。  此属性的类型为 <xref:System.ServiceModel.Security.SecurityKeyEntropyMode>。|  
|`issuedTokenRenewalThresholdPercentage`|可选的整数属性，指定在续订令牌之前可经过的有效时间段（由令牌颁发者提供）的百分比。  值的范围是 0 到 100。  默认值为 60，指定尝试续订之前经过了 60% 的时间。|  
|`issuerChannelBehaviors`|可选属性，指定当与颁发者进行通信时所使用的通道行为。|  
|`localIssuerChannelBehaviors`|可选属性，指定当与本地颁发者进行通信时所使用的通道行为。|  
|`maxIssuedTokenCachingTime`|可选的 Timespan 属性，指定当令牌颁发者 \(STS\) 未指定时间时，对颁发的令牌进行缓存的持续时间。  默认值为“10675199.02:48:05.4775807”。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<localIssuer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/localissuer.md)|指定令牌的本地颁发者地址以及用于与终结点进行通信的绑定。|  
|[\<issuerChannelBehaviors\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuerchannelbehaviors-element.md)|指定当联系本地颁发者时所使用的终结点行为。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<clientCredentials\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|指定用于向服务验证客户端身份的凭据。|  
  
## 备注  
 例如，颁发的令牌是在使用联合方案中的安全令牌服务 \(STS\) 进行身份验证时所使用的自定义凭据类型。  默认情况下，该令牌为 SAML 令牌。  有关详细信息，请参阅[联合令牌与颁发的令牌](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)。  和[联合令牌与颁发的令牌](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)。  
  
 本节包含用于配置本地令牌颁发者的元素，或者与安全令牌服务一起使用的行为。  有关配置客户端以使用本地令牌颁发机构的说明，请参见[如何：配置本地颁发者](../../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.IssuedTokenClientElement>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement.IssuedToken%2A>   
 <xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A>   
 <xref:System.ServiceModel.Security.IssuedTokenClientCredential>   
 [安全行为](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [联合令牌与颁发的令牌](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)   
 [保证客户端的安全](../../../../../docs/framework/wcf/securing-clients.md)   
 [如何：创建联合客户端](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [如何：配置本地颁发者](../../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)   
 [联合令牌与颁发的令牌](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)