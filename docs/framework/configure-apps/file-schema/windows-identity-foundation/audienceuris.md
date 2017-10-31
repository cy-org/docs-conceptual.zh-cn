---
title: "&lt;audienceUris&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7a3d8515-d756-4afe-a22d-07cbe2217ee3
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# &lt;audienceUris&gt;
指定的 Uri 是可接受的依赖方 \(RP\) 的标识符的集合。  标记将不被接受，除非它们的范围内允许的访问群体的 Uri 之一。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <audienceUris mode=xs:string>  
          <add value=xs:string />  
          <clear />  
          <remove value=xs:string />  
        </audienceUris>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|mode|<xref:System.IdentityModel.Selectors.AudienceUriMode>值，该值指定是否应将观众限制应用于传入令牌。  可能的值为"始终"，"从不"和"BearerKeyOnly"。  默认值为"总是"。  可选。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|`<add value=xs:string>`|添加指定的 URI `value` audienceUris 集合的属性。  需要 `value` 特性。  URI 是区分大小写。|  
|`<clear>`|清除 audienceUris 集合。  从集合中移除所有标识符。|  
|`<remove value=xs:string>`|删除所指定的 URI `value` audienceUris 集合中的属性。  需要 `value` 特性。  URI 是区分大小写。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|提供配置集合的安全令牌的处理程序。|  
  
## 备注  
 默认情况下该集合为空。 使用`<add>`， `<clear>`，和`<remove>`修改该集合的元素。  <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>和<xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>对象来配置任何观众 URI 集合中的值允许访问群体中的 URI 限制使用<xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement>对象。  
  
 `<audienceUris>`元素都由<xref:System.IdentityModel.Configuration.AudienceUriElementCollection>类。  添加到集合中的单个 URI 由<xref:System.IdentityModel.Configuration.AudienceUriElement>类。  
  
> [!NOTE]
>  使用`<audienceUris>`元素的子元素作为[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素已被否决，但仍然支持向后兼容性。  在设置`<securityTokenHandlerConfiguration>`元素会覆盖那些在`<identityConfiguration>`元素。  
  
## 示例  
 下面的 XML 说明如何配置应用程序的可接受观众的 Uri。  本示例配置单个的 URI。  此 URI 的范围内的标记将被接受，其他所有人都将被拒绝。  
  
```  
<audienceUris>  
  <add value="http://localhost:19851/"/>  
</audienceUris>  
```