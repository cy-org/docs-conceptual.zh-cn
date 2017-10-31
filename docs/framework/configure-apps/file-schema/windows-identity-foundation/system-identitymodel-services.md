---
title: "&lt;system.identityModel.services&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fa1624dd-2d74-4ae3-942e-498cee261ac5
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# &lt;system.identityModel.services&gt;
使用的 WS 联合身份验证协议进行身份验证的配置节。  
  
 \<system.identityModel.services\>  
  
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
 无  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md)|包含配置的设置<xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WSFAM\) 和<xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\) HTTP 模块。|  
  
### 父元素  
 无  
  
## 备注  
 添加`<system.identityModel.services>` SAM 和 WSFAM 提供设置应用程序的配置文件的部分。  
  
> [!IMPORTANT]
>  使用时<xref:System.IdentityModel.Services.ClaimsPrincipalPermission>或<xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute>类来提供基于声明的访问控制，在代码中，声明授权管理器 \(<xref:System.Security.Claims.ClaimsAuthorizationManager>\) 做出授权决定使用策略，通过配置和`<identityConfiguration>`隐式或显式地从引用的元素`<federationConfiguration>`本部分中的元素。  有关详细信息，请参阅**于**在[\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md)元素。  
  
 `<system.identityModel.services>`部分由<xref:System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection>类。  子集合`<federationConfiguration>`部分中配置的元素都由<xref:System.IdentityModel.Services.Configuration.FederationConfigurationElementCollection>类。  
  
## 示例  
 下面的 XML 说明如何添加`<system.identityModel.services>`配置文件的部分。  您必须首先将添加两个部分中声明`<system.identityModel.services>`节和`<system.identityModel>`节。  （当您添加`<system.identityModel.services>`部分中，您还应该添加一个声明为`<system.identityModel>`部分，确保默认`<identityConfiguration>`如有必要，可以由运行库创建截面。）已添加的节声明后，您可以配置下的联合身份验证设置`<system.identityModel.services>`元素。  
  
```  
<configuration>  
  <configSections>  
    <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
    <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
  </configSections>  
  
  <!-- Additional elements (not shown) -->  
  
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
  
</configuration>  
```