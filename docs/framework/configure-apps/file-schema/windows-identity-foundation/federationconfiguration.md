---
title: "&lt;federationConfiguration&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b14054c-6d07-46ab-ab58-03f14beac0f2
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 9
---
# &lt;federationConfiguration&gt;
配置<xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WSFAM\) 和<xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\) 时使用联合身份验证通过的 WS 联合身份验证协议。  配置<xref:System.Security.Claims.ClaimsAuthorizationManager>时使用<xref:System.IdentityModel.Services.ClaimsPrincipalPermission>或<xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute>类来提供基于声明的访问控制。  
  
## 语法  
  
```  
<system.identityModel.services>  
  <federationConfiguration name=xs:string identityConfigurationName=xs:string>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|name|此联合身份验证配置元素的名称。  此属性主要用于将来的协议提供了扩展点。  可选。|  
|identityConfigurationName|标识配置部分中指定的名称[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)使用的元素。  如果未指定此属性，则使用默认标识配置节。  可选。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<cookieHandler\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/cookiehandler.md)|配置使用的 SAM 的 cookie 处理程序。  可选。|  
|[\<serviceCertificate\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/servicecertificate.md)|配置的证书，用来加密和解密的标记。  可选。|  
|[\<wsFederation\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/wsfederation.md)|配置 WS 联合身份验证的身份验证模块 \(WSFAM\)。  可选。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<system.identityModel.services\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md)|使用的 WS 联合身份验证协议进行身份验证的配置节。|  
  
## 备注  
 \<federationConfiguration\> 元素提供了两个不同的方案中的设置：  
  
-   在被动的 Web 应用程序中使用 WS 联合身份验证时，该元素包含设置配置<xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WSFAM\) 和<xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\)。  它还引用标识配置为用于配置安全标记处理程序和证书和组件 （如索赔授权管理器和声明的身份验证管理器。  
  
-   当使用<xref:System.IdentityModel.Services.ClaimsPrincipalPermission>或<xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute>提供基于声明的访问控制，在代码中的类、 元素引用标识配置配置索赔授权管理器和策略，用于做出授权决定的。  是这样，即使在不是被动的 Web 方案 ； 方案中 例如，Windows 资格） 应用程序或不是基于 Web 的应用程序。  如果应用程序不是被动的 Web 应用程序中， [\<claimsAuthorizationManager\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimsauthorizationmanager.md)元素 （和它的子策略元素，如果有的话） 由引用标识配置的`<federationConfiguration>`元素所应用的唯一设置。  所有其他属性都将被忽略。  
  
 而无需考虑的情况下，运行库将加载默认的联合身份验证配置。  该行为的定义如下：  
  
1.  如果没有任何`<federationConfiguration>`元素存在，运行时创建一个联合身份验证配置并填充它的默认值。  此默认联合身份验证配置将引用的默认标识配置。  
  
2.  如果一个`<federationConfiguration>`的元素，则无论是否被命名或未命名的默认联合身份验证配置。  如果其`identityConfiguration`属性指定，则引用的命名的标识配置 ； 否则，默认标识配置中被引用。  
  
3.  如果未命名`<federationConfiguration>`的元素，它是默认的联合身份验证配置。  如果其`identityConfiguration`属性指定，则引用的命名的标识配置 ； 否则，默认标识配置中被引用。  
  
4.  如果多个名为`<federationConfiguration>`元素都存在并不是未命名`<federationConfiguration>`的元素，则引发异常。  
  
 通常情况下，只有一个`<federationConfiguration>`定义部分。  本部分是默认的联合身份验证配置。  您可以指定多个唯一命名`<federationConfiguration>`元素本身。 但是，在这种情况下，如果要加载之外的其他未命名的联合身份验证配置，则必须提供的处理程序。  <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfigurationCreated>事件和集<xref:System.IdentityModel.Services.Configuration.FederationConfigurationCreatedEventArgs.FederationConfiguration%2A?displayProperty=fullName>到处理程序内的属性<xref:System.IdentityModel.Services.Configuration.FederationConfiguration>对象中相应的值初始化`<federationConfiguration>`配置文件中的元素。  
  
 `<federationConfiguration>`元素都由<xref:System.IdentityModel.Services.Configuration.FederationConfigurationElement>类。  配置对象本身由<xref:System.IdentityModel.Services.Configuration.FederationConfiguration>类。  一个<xref:System.IdentityModel.Services.Configuration.FederationConfiguration>实例上设置<xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName>属性，并提供联合应用程序配置。  
  
## 示例  
 所示的 XML `<federationConfiguration>`元素的指定设置 WSFAM，并指定的默认 cookie 的处理程序 （实例的<xref:System.IdentityModel.Services.ChunkedCookieHandler>类） 由 SAM。  
  
> [!WARNING]
>  在此示例中，cookie 的处理程序和 WSFAM 都不需要使用 HTTPS。  这是因为`requireHttps`属性上`<wsFederation>`元素和`requireSsl`属性上`<cookieHandlerElement>`是`false`。  这些设置不是建议大多数生产环境，因为它们可能会带来安全风险。  
  
```  
<system.identityModel.services>  
  <federationConfiguration>  
    <wsFederation passiveRedirectEnabled="true"   
      issuer="http://localhost:15839/wsFederationSTS/Issue"   
      realm="http://localhost:50969/" reply="http://localhost:50969/"   
      requireHttps="false"   
      signOutReply="http://localhost:50969/SignedOutPage.html"   
      signOutQueryString="Param1=value2&Param2=value2"   
      persistentCookiesOnPassiveRedirects="true" />  
    <cookieHandler requireSsl="false" />  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## 请参阅  
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>   
 <xref:System.IdentityModel.Services.SessionAuthenticationModule>   
 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName>   
 [\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)