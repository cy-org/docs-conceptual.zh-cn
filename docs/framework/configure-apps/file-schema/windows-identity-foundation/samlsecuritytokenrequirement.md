---
title: "&lt;samlSecurityTokenRequirement&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 09202d12-88d3-49cc-953b-703bcc1690eb
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# &lt;samlSecurityTokenRequirement&gt;
为 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> 选件类、 <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> 选件类或这些选件类之一的派生类提供配置。  由 <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> 选件类。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add>  
        <samlSecurityTokenRequirement   
            issuerCertificateValidationMode="None||ChainTrust||PeerTrust||PeerOrChainTrust||Custom"  
            issuerCertificateRevocationMode="NoCheck||Offline||Online"  
            issuerCertificateTrustedStoreLocation="CurrentLocation||LocalMachine"  
            issuerCertificateValidator="Namespace.Class Assembly"  
            mapToWindows=xs:boolean  
          <nameClaimType value=xs:string />  
          <roleClaimType value=xs:string />  
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
|mapToWindows|指定标记处理程序通过使用传入的UPN声明，是否应映射该验证的标记与Windows帐户。  默认值为“false”。|  
|issuerCertificateRevocationMode|指定吊销模式为X.509证书使用的 <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> 值。  默认值为“联机”。|  
|issuerCertificateValidationMode|指定验证模式为X.509证书使用的 <xref:System.ServiceModel.Security.X509CertificateValidationMode> 值。  默认值为“PeerOrChainTrust”。|  
|issuerCertificateTrustedStoreLocation|指定X.509证书存储区的 <xref:System.Security.Cryptography.X509Certificates.StoreLocation> 值。  默认值为“LocalMachine”。|  
|issuerCertificateValidator|从 <xref:System.IdentityModel.Selectors.X509CertificateValidator>派生的自定义类型。  如果 `issuerCertificateValidationMode` 特性为“custom”，该类型的实例为颁发者证书验证。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<nameClaimType\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/nameclaimtype.md)|设置指定 <xref:System.Security.Principal.IIdentity.Name%2A> 属性的声明类型。|  
|[\<roleClaimType\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/roleclaimtype.md)|指定定义在 <xref:System.Security.Claims.ClaimsIdentity> 对象的集合的角色类型声明标记处理程序的 <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ValidateToken%2A> 方法返回的声明类型。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/add.md)|将指定的安全标记处理程序添加到标记处理程序集合。|  
  
## 备注  
 `<samlSecurityTokenRequirement>` 元素由对象模型的 <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> 选件类表示和用于配置在 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> 或 <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>的 `SamlSecurityTokenRequirement` 属性。  
  
## 示例  
  
```  
<add type="System.IdentityModel.Tokens.SamlSecurityTokenHandler, System.IdentityModel">  
    <samlSecurityTokenRequirement issuerCertificateValidationMode="PeerOrChainTrust"  
                                  issuerCertificateRevocationMode="Online"  
                                  issuerCertificateTrustedStoreLocation="LocalMachine"  
                                  mapToWindows="false">  
  
        <nameClaimType value="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" />  
        <roleClaimType value="schemas.microsoft.com/ws/2006/04/identity/claims/role" />  
    </samlSecurityTokenRequirement>  
</add>  
```