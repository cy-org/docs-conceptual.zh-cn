---
title: "&lt;issuerNameRegistry&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58b39d12-c953-40c4-88af-d7eb3343ca28
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 12
---
# &lt;issuerNameRegistry&gt;
配置颁发者名称注册表所使用的标记处理程序集合中的处理程序。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerNameRegistry type=xs:string>  
          <optionalCustomConfigurationElements />  
        </issuerNameRegistry>  
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
|type|从派生类型<xref:System.IdentityModel.Tokens.IssuerNameRegistry>类。  有关如何指定自定义`type`，请参阅[Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences)。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<trustedIssuers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/trustedissuers.md)|当`type`属性指定基于配置的颁发者名称注册表 \( <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>类）、 [\<trustedIssuers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/trustedissuers.md)元素，必须指定。  [\<trustedIssuers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/trustedissuers.md)元素可以采用`<add>`， `<clear>`，或`<remove>`作为子元素的元素。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|提供配置集合的安全令牌的处理程序。|  
  
## 备注  
 颁发者的所有标记都验证使用颁发者名称的注册表。  这是一个从派生的对象<xref:System.IdentityModel.Tokens.IssuerNameRegistry>类。  颁发者名称注册表用于将所需验证签名的标记生成相应的颁发者的加密材料助记符名称相关联。  颁发者名称注册表维护依赖方 \(RP\) 应用程序都受信任的颁发者的列表。  使用指定的颁发者名称注册表类型`type`属性。  `<issuerNameRegistry>`元素可以有一个或多个提供配置为指定类型的子元素。  您提供通过重写处理这些子元素的逻辑<xref:System.IdentityModel.Tokens.IssuerNameRegistry.LoadCustomConfiguration%2A>方法。  
  
 提供了单一的颁发者名称的注册表类型的框中，WIF <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>类。  此类使用受信任的颁发者的证书配置中指定的一组。  它要求子配置元素， `<trustedIssuers>`，在配置受信任的颁发者的证书的集合。  受信任的证书使用 ASN.1 编码形式的证书指纹和添加或从集合中移除通过指定`<add>`， `<clear>`，或`<remove>`元素。  
  
 `<issuerNameRegistry>`元素都由<xref:System.IdentityModel.Configuration.IssuerNameRegistryElement>类。  
  
> [!NOTE]
>  指定`<issuerNameRegistry>`元素的子元素作为[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素已被否决，但仍然支持向后兼容性。  在设置`<securityTokenHandlerConfiguration>`元素会覆盖那些在`<identityConfiguration>`元素。  
  
## 示例  
 下面的 XML 说明如何指定配置基于颁发者名称的注册表。  
  
```  
<issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
  <trustedIssuers>  
    <add thumbprint="9B74CB … 1EF40D0" name="LocalSTS" />  
  </trustedIssuers>  
</issuerNameRegistry>  
  
```  
  
## 请参阅  
 <xref:System.IdentityModel.Tokens.IssuerNameRegistry>   
 <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>