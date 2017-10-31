---
title: "&lt;certificateValidation&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c54c704-b55e-4631-88ff-4d4a5621554c
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# &lt;certificateValidation&gt;
控件标记处理程序使用验证证书的设置。  ，如果特定的处理程序配置了自己的验证，这些设置重写。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <certificateValidation  
      certificateValidationMode="None||ChainTrust||PeerTrust||PeerOrChainTrust||Custom"  
      revocationMode="NoCheck||Offline||Online"  
      trustedStoreLocation="CurrentLocation||LocalMachine" >  
    </certificateValidation>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|certificateValidationMode|指定验证模式为 X.509 证书使用的 <xref:System.ServiceModel.Security.X509CertificateValidationMode> 值。  默认值为 “PeerOrChainTrust”。  使用元素，若要指定自定义验证程序，请将此属性设置为 “custom”并指定该验证程序 [\<certificateValidator\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/certificatevalidator.md) 。  选项。|  
|revocationMode|指定吊销模式为 X.509 证书使用的 <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> 值。  默认值为 “联机”。  选项。|  
|trustedStoreLocation|指定 X.509 证书存储区的 <xref:System.Security.Cryptography.X509Certificates.StoreLocation> 值。  默认值为 “LocalMachine”。  选项。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<certificateValidator\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/certificatevalidator.md)|用于证书验证指定自定义类型。  此类型，仅当元素的 `certificateValidationMode` 属性 [\<certificateValidation\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/certificatevalidation.md) 设置为 “custom”，请使用。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|指定服务级别的标识设置。|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|出于安全标记处理程序的集合提供配置。|  
  
## 备注  
 `<certificateValidation>` 元素既可以在服务级别在 `<identityConfiguration>` 元素下或在 `<securityTokenHandlerConfiguration>` 元素下的安全标记处理程序集合级别。  在服务重写这些指定的标记处理程序集合的设置。  一些标记处理程序在其配置为允许您指定证书验证设置。  在各个标记处理程序中的设置重写这些指定了服务级别和在安全标记处理程序集合。  
  
## 示例  
  
```  
<certificateValidation certificateValidationMode="PeerOrChainTrust"  
                       revocationMode="Online"  
                       trustedStoreLocation="LocalMachine" />  
```