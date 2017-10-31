---
title: "&lt;trustedIssuers&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d818c917-07b4-40db-9801-8676561859fd
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;trustedIssuers&gt;
配置受信任的颁发者证书使用的基于配置的颁发者名称注册表列表 \(<xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>\)。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerNameRegistry>  
          <trustedIssuers>  
            <add thumbprint=xs:string name=xs:string>  
            <clear>  
            <remove thumbprint=xs:string>  
          </trustedIssuers>  
        </issuerNameRegistry>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
 无  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|`<add thumbprint=xs:string name=xs:string>`|将证书添加到受信任的颁发者的集合。  证书用指定的`thumbprint`属性。  此属性是必需的并应包含证书指纹的 ASN.1 编码形式。  `name`属性是可选的可用于指定证书的友好名称。|  
|`<clear>`|清除集合中的受信任的颁发者的所有证书。|  
|`<remove thumbprint=xs:string>`|从受信任的颁发者的集合中移除证书。  证书用指定的`thumbprint`属性。  此特性必选。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<issuerNameRegistry\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/issuernameregistry.md)|配置注册表颁发者名称。 **Important:**  `type`属性的`<issuerNameRegistry>`元素必须引用<xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>类的`<trustedIssuers>`是有效的元素。|  
  
## 备注  
 Windows 标识基础 \(WIF\) 提供的一个实现<xref:System.IdentityModel.Tokens.IssuerNameRegistry>类现成的<xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>类。  配置颁发者名称注册表维护从配置中加载的受信任的颁发者的列表。  列表将每个颁发者名称相关联的 X.509 证书所需验证令牌所产生的颁发者的签名。  受信任的颁发者的证书列表下指定`<trustedIssuers>`元素。  列表中的每个元素将助记键的颁发者名称与所需验证签名的标记生成该颁发者的 X.509 证书。  受信任证书指定使用 ASN.1 编码形式的证书指纹，和通过使用集合添加`<add>`元素。  您可以清除或删除列表中的颁发者 （证书），通过使用`<clear>`和`<remove>`元素。  
  
 `type`属性的`<issuerNameRegistry>`元素必须引用<xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>类的`<trustedIssuers>`是有效的元素。  
  
## 示例  
 下面的 XML 说明如何指定配置基于颁发者名称的注册表。  
  
```  
<issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
  <trustedIssuers>  
    <add thumbprint="9B74CB2F32 … B1DC01EF40D0" name="LocalSTS" />  
  </trustedIssuers>  
</issuerNameRegistry>  
  
```  
  
## 请参阅  
 <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>   
 <xref:System.IdentityModel.Tokens.IssuerNameRegistry>