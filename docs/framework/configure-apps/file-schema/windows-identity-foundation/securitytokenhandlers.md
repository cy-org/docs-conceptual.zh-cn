---
title: "&lt;securityTokenHandlers&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f11a631d-4094-4e11-bb03-4ede74b30281
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;securityTokenHandlers&gt;
指定的安全令牌的处理程序中注册该终结点的集合。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|name|指定标记处理程序集合的名称。  识别的框架的唯一值是"ActAs"和"OnBehalfOf"。  如果使用这些名称的任何一个指定标记处理程序集合，分别处理 ActAs 或 OnBehalfOf 令牌时，将使用集合。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/add.md)|安全标记处理程序添加的标记处理程序集合。|  
|[\<clear\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/clear.md)|清除标记处理程序集合中的所有安全令牌处理。|  
|[\<remove\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/remove.md)|从标记处理程序集合中移除安全标记处理程序。|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|提供了配置标记处理程序的集合。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|指定的服务级别标识设置。|  
  
## 备注  
 在服务配置，您可以指定一个或多个安全标记处理程序的命名的集合。  您可以使用指定的集合名称`name`属性。  该框架还处理的唯一名称是"ActAs"和"OnBehalfOf"。  如果在这些集合中存在的处理程序，它们由安全令牌服务 \(STS\) 的默认处理程序而不是在处理`ActAs`和`OnBehalfOf`的标记。  
  
 默认情况下该集合填充与以下处理程序类型： <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>， <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>， <xref:System.IdentityModel.Tokens.KerberosSecurityTokenHandler>， <xref:System.IdentityModel.Tokens.WindowsUserNameSecurityTokenHandler>， <xref:System.IdentityModel.Tokens.RsaSecurityTokenHandler>， <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>，和<xref:System.IdentityModel.Tokens.EncryptedSecurityTokenHandler>。  您可以修改该集合使用`<add>`， `<remove>`，和`<clear>`元素。  您必须确保只有单个处理程序的任何特定类型存在于集合中。  例如，如果您派生处理程序与<xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>类，或者您的处理程序或<xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>可能在一个集合，但不能同时配置。  
  
 使用`<securityTokenHandlerConfiguration>`元素集合中指定的处理程序的配置设置。  通过此元素指定的设置会覆盖那些指定的服务通过[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素。  某些 （包括几个内置的处理程序类型） 的处理程序可以支持其他配置的子元素通过`<add>`元素。  在处理程序指定的设置重写指定集合或该服务上的等效设置。