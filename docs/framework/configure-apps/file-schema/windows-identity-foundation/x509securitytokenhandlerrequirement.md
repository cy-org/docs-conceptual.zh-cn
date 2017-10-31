---
title: "&lt;x509SecurityTokenHandlerRequirement&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: aca22c2c-5ae7-42af-9bbd-15c2524692ce
caps.latest.revision: 3
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 3
---
# &lt;x509SecurityTokenHandlerRequirement&gt;
为 <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler> 选件类或派生类提供选项配置。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add type="System.IdentityModel.Tokens.X509SecurityTokenHandler, System.IdentityModel">  
        <x509SecurityTokenHandlerRequirement>  
          mapToWindows=xs:boolean  
          certificateValidationMode="None||ChainTrust||PeerTrust||PeerOrChainTrust||Custom"  
          certificateValidator="Namespace.Class, Assembly"  
          revocationMode="NoCheck||Offline||Online"  
          trustedStoreLocation="CurrentUser||LocalMachine"  
        </x509SecurityTokenHandlerRequirement>  
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
|certificateValidationMode|指定验证模式为X.509证书使用的 <xref:System.ServiceModel.Security.X509CertificateValidationMode> 值。  默认值为“PeerOrChainTrust”。|  
|mapToWindows|指定标记处理程序通过使用传入的UPN声明，是否应映射该验证的标记与Windows帐户。  默认值为“false”。|  
|revocationMode|指定吊销模式为X.509证书使用的 <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> 值。  默认值为“联机”。|  
|trustedStoreLocation|指定X.509证书存储区的 <xref:System.Security.Cryptography.X509Certificates.StoreLocation> 值。  默认值为“LocalMachine”。|  
|certificateValidator|从 <xref:System.IdentityModel.Selectors.X509CertificateValidator>派生的自定义类型。  如果 `certificateValidationMode` 特性为“custom”，该类型的实例为颁发者证书验证。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/add.md)|将指定的安全标记处理程序添加到标记处理程序集合。|  
  
## 示例  
  
```  
<add type="System.IdentityModel.Tokens.X509SecurityTokenHandler, System.IdentityModel">  
    <x509SecurityTokenHandlerRequirement mapToWindows="true"   
                                         certificateValidationMode="PeerOrChainTrust"   
                                         revocationMode="Online"   
                                         trustedStoreLocation="LocalMachine" />  
</add>  
```