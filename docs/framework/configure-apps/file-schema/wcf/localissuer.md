---
title: "&lt;localIssuer&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 26bdd0df-0e7d-4b9e-bbeb-f28c53769385
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;localIssuer&gt;
指定要用于颁发安全令牌的本地颁发者的地址和绑定。  
  
## 语法  
  
```  
  
<localIssuer address="string"  
      binding="string"  
      bindingConfiguration="string" />  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|address|必选字符串。  指定本地颁发者的 URI。|  
|绑定|可选的字符串。  系统提供的一个绑定。  有关列表，请参见 [系统提供的绑定](../../../../../docs/framework/wcf/system-provided-bindings.md)。|  
|bindingConfiguration|可选的字符串。  指定在配置文件中找到的绑定配置。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<标识\>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|指定此本地颁发者的标识信息。|  
|[\<页眉\>](../../../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md)|地址头的集合，要正确书写本地颁发者的地址必须使用这些地址头。  可以使用 `add` 关键字向此集合添加标头。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<issuedToken\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md)|指定用于向服务验证客户端身份的自定义令牌。|  
  
## 备注  
 从安全令牌服务 \(STS\) 获取已颁发的令牌时，必须使用地址和绑定配置客户端应用程序，以将其用于与 STS 进行通信。  如果 <xref:System.ServiceModel.WSFederationHttpBinding> 没有为安全令牌服务提供 URL，或者联合绑定的颁发者地址为 http:\/\/schemas.microsoft.com\/2005\/12\/ServiceModel\/Addressing\/Anonymous 或 `null`，则客户端的 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 通道使用由 `address` 和 `binding` 指定的值与 STS 进行通信，以获取颁发的令牌。  有关配置本地颁发者的更多信息，请参见[如何：配置本地颁发者](../../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)。  
  
## 示例  
 下面的示例设置 `localIssuer` 元素的 `address`、`binding` 和 `bindingConfiguration` 属性。  
  
```  
<system.serviceModel>  
 <behaviors>  
 <endpointBehaviors>  
  <behavior name="MyEndpointBehavior">  
   <clientCredentials>  
    <issuedToken cacheIssuedTokens="false"   
                 defaultKeyEntropyMode="ClientEntropy">  
     <localIssuer address="net.tcp://cohowinery/tokens"   
                  binding="netTcpBinding"  
                  bindingConfiguration="myTcpBindingConfig" />  
    </issuedToken>  
   </clientCredentials>  
  </behavior>  
  </endpointBehaviors>  
  </behaviors>  
</system.serviceModel>  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.IssuedTokenClientElement.LocalIssuer%2A>   
 <xref:System.ServiceModel.Configuration.IssuedTokenParametersEndpointAddressElement>   
 <xref:System.ServiceModel.Security.IssuedTokenClientCredential>   
 [安全行为](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [如何：配置本地颁发者](../../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)   
 [服务标识和身份验证](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)   
 [安全行为](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [联合令牌与颁发的令牌](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [保证客户端的安全](../../../../../docs/framework/wcf/securing-clients.md)   
 [如何：创建联合客户端](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [联合令牌与颁发的令牌](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)