---
title: "&lt;certificateReference&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2ac8bc14-e9f1-48fb-b662-f5991558fbe4
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# &lt;certificateReference&gt;
指定用于查找和验证的 X.509 证书的证书存储区中的设置。  
  
## 语法  
  
```  
<system.identityModel.services>  
  <federationConfiguration>  
    <serviceCertificate>  
      <certificateReference   
        storeName=”AddressBook||AuthRoot||CertificateAuthority||Disallowed||My||Root||TrustedPeople||TrustedPublisher”  
        storeLocation=”CurrentUser||LocalMachine”  
        x509FindType="FindByThumbprint||FindBySubjectName||FindBySubjectDistinguishedName||FindByIssuerName||FindByIssuerDistinguishedName||FindBySerialNumber||FindByTimeValid||FindByTimeNotYetValid||FindByTimeExpired||FindByTemplateName||FindByApplicationPolicy||FindByCertificatePolicy||FindByExtension||FindByKeyUsage||FindBySubjectKeyIdentifier"  
        findValue=xs:String  
        isChainIncluded=xs:Boolean >  
      </certificateReference>  
    </serviceCertificate>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|storeName|X.509 证书存储区的名称。  默认值是"我"。  可选。|  
|storeLocation|A <xref:System.Security.Cryptography.X509Certificates.StoreLocation>的值，指定的 X.509 证书存储区位置。  默认值为"LocalMachine"。  可选。|  
|x509FindType|<xref:System.Security.Cryptography.X509Certificates.X509FindType>的值，指定要执行的搜索的类型。  默认为"FindBySubjectDistinguishedName"。  可选。|  
|findValue|要在 X.509 证书存储区中搜索的值。  可选。|  
|isChainIncluded|指定是否应通过使用证书链执行验证。  默认值为"true"。 通过使用证书链执行验证。  可选。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<serviceCertificate\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/servicecertificate.md)|配置的证书，用来加密和解密的标记。|  
  
## 备注  
 `<certificateReference>`元素指定用于查找和验证的 X.509 证书的证书存储区中的设置。  指定的子元素时`<serviceCertficate>`元素，它指定用于加密和解密令牌的 X.509 证书的位置和验证设置。  `<certificateReference>`元素都由<xref:System.ServiceModel.Configuration.CertificateReferenceElement>类。