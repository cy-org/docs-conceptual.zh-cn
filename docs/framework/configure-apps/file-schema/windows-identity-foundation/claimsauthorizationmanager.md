---
title: "&lt;claimsAuthorizationManager&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9354eee3-f692-4ad6-8427-3169686b8bcc
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;claimsAuthorizationManager&gt;
为传入的声明的声明授权管理器中注册。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <claimsAuthorizationManager type = xs:string>  
      <optionalConfigurationElements />  
    </claimsAuthorizationManager>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|type|自定义类型派生自的<xref:System.Security.Claims.ClaimsAuthorizationManager>类。  有关如何指定`type`属性，请参阅[Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences)。|  
  
### 子元素  
 如果没有`type`属性中，如果`type`属性引用<xref:System.Security.Claims.ClaimsAuthenticationManager>类， `<claimsAuthorizationManager>`元素不会子元素 ； 但是，从派生类<xref:System.Security.Claims.ClaimsAuthorizationManager>可以定义子配置元素。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|指定的服务级别标识设置。|  
  
## 备注  
 通过提供的默认行为<xref:System.Security.Claims.ClaimsAuthorizationManager>类始终授权传入的声明。  如果不是`type`指定属性或`type`属性指定了<xref:System.Security.Claims.ClaimsAuthorizationManager>类， `<claimsAuthorizationManager>`元素不会子元素。  您可以指定`type`属性，以注册类型派生自<xref:System.Security.Claims.ClaimsAuthorizationManager>类可以实现自定义行为。  派生的类可以支持配置的子元素通过`<claimsAuthorizationManager>`元素，通过重写<xref:System.Security.Claims.ClaimsAuthorizationManager.LoadCustomConfiguration%2A>方法来处理这些元素。  定义的子元素的架构由设计器的类。  
  
> [!IMPORTANT]
>  使用时<xref:System.IdentityModel.Services.ClaimsPrincipalPermission>或<xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute>类来提供基于声明的访问控制，在代码中，所引用的标识配置`<federationConfiguration>`元素配置的索赔授权管理器和策略，用于做出授权决定。  是这样，即使在不是被动的 Web 方案，例如 Windows 资格） 应用程序或不是基于 Web 的应用程序的方案中。  如果应用程序不是被动的 Web 应用程序中， `<claimsAuthorizationManager>`元素 （和它的子策略元素，如果有的话） 的引用的标识配置将应用的唯一设置。  所有其他设置都被忽略。  有关更多信息，请参见 [\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md) 元素。  
  
 此元素设置<xref:System.IdentityModel.Configuration.IdentityConfiguration.ClaimsAuthorizationManager%2A?displayProperty=fullName>属性。  
  
## 示例  
 下面的 XML 说明索赔授权的配置管理器的实现的策略组成的资源操作对每个指定的请求者必须拥有对资源执行的操作的声明的布尔组合。  在中找不到实现声明授权管理器可以使用此策略的代码`ClaimsBasedAuthorization`的示例。  
  
```  
<system.identityModel>  
    <identityConfiguration>  
      <claimsAuthorizationManager type="ClaimsAuthorizationLibrary.MyClaimsAuthorizationManager, ClaimsAuthorizationLibrary">  
        <policy resource="http://localhost:28491/Developers.aspx" action="GET">  
          <or>  
            <claim claimType="http://schemas.microsoft.com/ws/2008/06/identity/claims/role" claimValue="developer" />  
            <claim claimType="http://schemas.xmlsoap.org/claims/Group" claimValue="Administrator" />  
          </or>  
        </policy>  
        <policy resource="http://localhost:28491/Administrators.aspx" action="GET">  
          <and>  
            <claim claimType="http://schemas.xmlsoap.org/claims/Group" claimValue="Administrator" />  
            <claim claimType="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country" claimValue="USA" />  
          </and>  
        </policy>  
        <policy resource="http://localhost:28491/Default.aspx" action="GET">  
        </policy>  
        <policy resource="http://localhost:28491/" action="GET">  
        </policy>  
        <policy resource="http://localhost:28491/Claims.aspx" action="GET">  
        </policy>  
      </claimsAuthorizationManager>  
    <identityConfiguration>  
<system.identityModel>  
```