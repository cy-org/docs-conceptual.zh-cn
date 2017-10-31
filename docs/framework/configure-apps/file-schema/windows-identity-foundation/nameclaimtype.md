---
title: "&lt;nameClaimType&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 17514d95-f0f5-4789-8e28-346640dc227c
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# &lt;nameClaimType&gt;
设置指定 <xref:System.Security.Principal.IIdentity.Name%2A> 属性的声明类型。  声明类型用于搜索在 <xref:System.Security.Claims.ClaimsIdentity> 对象的集合中 <xref:System.Security.Claims.Claim> 此标记处理程序 <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ValidateToken%2A> 方法返回的。  匹配的声明的值然后设置，此标记处理程序生成的 <xref:System.Security.Principal.IIdentity> 的名称。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add>  
        <samlSecurityTokenRequirement>  
          <nameClaimType value=xs:string>  
          </nameClaimType>  
        </samlSecurityTokenRequirement>  
      </add>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|value|指定URI表示声明的声明类型为 <xref:System.Security.Principal.IIdentity.Name%2A> 属性的字符串。  必选。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<samlSecurityTokenRequirement\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/samlsecuritytokenrequirement.md)|为 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> 选件类、 <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> 选件类或这些选件类之一的派生类提供配置。|  
  
## 备注  
 ，当 <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> 对象从配置时，初始化 `<nameClaimType>` 元素将设置 <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement.NameClaimType%2A> 属性。  
  
## 示例  
  
```  
<add type="System.IdentityModel.Tokens.SamlSecurityTokenHandler, System.IdentityModel">  
    <samlSecurityTokenRequirement>  
        <nameClaimType value="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" />  
    </samlSecurityTokenRequirement>  
</add>  
```  
  
## 请参阅  
 <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement.NameClaimType%2A>