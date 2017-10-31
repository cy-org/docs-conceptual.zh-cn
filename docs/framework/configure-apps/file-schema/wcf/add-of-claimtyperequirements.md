---
title: "&lt;claimTypeRequirements&gt; 的 &lt;add&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c68e83c9-39e8-4264-b1ce-b6a9eb5b98aa
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# &lt;claimTypeRequirements&gt; 的 &lt;add&gt;
指定希望出现在联合凭据中的必选和可选的声明类型。  例如，服务规定有关传入凭据的要求，传入凭据必须具有某组声明类型。  
  
## 语法  
  
```  
  
<claimTypeRequirements>  
      <add claimType="URI"  
           isOptional="Boolean" />  
</claimTypeRequirements>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|claimType|一个 URI，定义声明类型。  例如，若要从网站上购买产品，用户必须提供具有足够信用额度的有效信用卡。  声明类型将为信用卡 URI。|  
|isOptional|一个布尔值，指定声明是否为可选的。  如果声明是必选的，则将此属性设置为 `false`。<br /><br /> 当服务请求一些并非必要的信息时，可以使用此属性。  例如，您可以要求用户输入其名、姓和地址，但决定其电话号码是可选的。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<claimTypeRequirements\>](../../../../../docs/framework/configure-apps/file-schema/wcf/claimtyperequirements-element.md)|指定所需声明类型的集合。<br /><br /> 在联合方案中，服务规定有关传入凭据的要求。  例如，传入凭据必须具有某组声明类型。  此集合中的每个元素都指定希望出现在联合凭据中的必选和可选的声明类型。|  
  
## 备注  
 在联合方案中，服务规定有关传入凭据的要求。  例如，传入凭据必须具有某组声明类型。  此要求出现在安全策略中。  当客户端请求来自联合服务（例如 CardSpace）的凭据时，它会将要求放置在令牌请求 \(RequestSecurityToken\) 中，以便联合服务能够相应地颁发符合要求的凭据。  
  
## 示例  
 下面的配置将两个声明类型要求添加到安全绑定。  
  
```  
<bindings>  
    <wsFederationHttpBinding>  
      <binding name="myFederatedBinding">  
        <security mode="Message">  
          <message issuedTokenType="urn:oasis:names:tc:SAML:1.0:assertion">  
            <claimTypeRequirements>  
              <add claimType=  
"http://schemas.microsoft.com/ws/2005/05/identity/claims/EmailAddress"/>  
              <add claimType=  
"http://schemas.microsoft.com/ws/2005/05/identity/claims/UserName"    
optional="true" />  
            </claims>  
          </message>  
        </security>  
      </binding>  
    </wsFederationHttpBinding>  
</bindings>  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Security.Tokens.ClaimTypeRequirement>   
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters.ClaimTypeRequirements%2A>   
 <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement.ClaimTypeRequirements%2A>   
 <xref:System.ServiceModel.Configuration.ClaimTypeElementCollection>   
 <xref:System.ServiceModel.Configuration.ClaimTypeElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [\<claimTypeRequirements\>](../../../../../docs/framework/configure-apps/file-schema/wcf/claimtyperequirements-element.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [扩展绑定](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [自定义绑定](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [如何：使用 SecurityBindingElement 创建自定义绑定](../../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)   
 [自定义绑定安全性](../../../../../docs/framework/wcf/samples/custom-binding-security.md)