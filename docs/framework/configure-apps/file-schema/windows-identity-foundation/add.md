---
title: "&lt;add&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4712a888-f154-4395-8887-ef14a88a6497
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;add&gt;
标记处理程序集合添加指定的安全令牌的处理程序。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add type=xs:string>  
        <optionalConfigurationElement>  
        </optionalConfigurationElement>  
      </add>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|type|要添加的标记处理程序的 CLR 类型名称。  有关如何指定`type`属性，请参阅[Custom Type References](http://msdn.microsoft.com/zh-cn/7286d2e3-c63d-49fd-abdc-ce2705f22c24)。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<samlSecurityTokenRequirement\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/samlsecuritytokenrequirement.md)|提供了有关配置<xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>类， <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>类或派生的类，这些类的两个。|  
|[\<sessionTokenRequirement\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/sessiontokenrequirement.md)|提供了有关配置<xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>类或派生的类。|  
|[\<userNameSecurityTokenHandlerRequirement\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/usernamesecuritytokenhandlerrequirement.md)|提供了有关配置<xref:System.IdentityModel.Services.Tokens.MembershipUserNameSecurityTokenHandler>类或派生的类。|  
|[\<x509SecurityTokenHandlerRequirement\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/x509securitytokenhandlerrequirement.md)|提供了可选配置的<xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>类或派生的类。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<securityTokenHandlers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlers.md)|指定的安全令牌的处理程序中注册该终结点的集合。|  
  
## 备注  
 `<add>`元素可以采取指定的标记处理程序的配置包含一个子元素。  这是依赖于通过的处理程序类的引用是否`type`属性的`<add>`元素提供支持此功能。  标记处理程序类，提供此功能，必须公开的构造函数<xref:System.Xml.XmlElement>对象。  
  
```  
public class CustomTokenHandler : Microsoft.IdentityModel.Tokens.SecurityTokenHandler  
{  
    public CustomTokenHandler( XmlElement customConfig )  
    {  
    }  
}  
```  
  
 几个内置的安全令牌的处理程序类并提供此功能。  These classes are <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>, <xref:System.IdentityModel.Services.Tokens.MembershipUserNameSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>, and <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>.  
  
> [!IMPORTANT]
>  标记处理程序集合只能包含单个处理任何的程序给定的类型。  这意味着，例如，如果您想要添加的处理程序从派生的<xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>类的集合，必须首先删除<xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>，则默认情况下显示从集合中。  您可以使用[\<remove\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/remove.md)元素中移除单个处理程序集合或使用[\<clear\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/clear.md)元素从集合中移除所有事件处理程序。  
  
 在处理程序指定的设置重写下标记处理程序集合中指定的等效设置[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)元素，并在下的服务级别指定的[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素。  
  
## 示例  
 下面的 XML 显示如何使用`<add>`和`<remove>`来替换默认的会话令牌处理程序使用自定义会话标记处理程序元素。  XML 取自`ClaimsAwareWebFarm`的示例。  
  
```  
<securityTokenHandlers>  
  <remove type="System.IdentityModel.Tokens.SessionSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
  <add type="System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
</securityTokenHandlers>  
```