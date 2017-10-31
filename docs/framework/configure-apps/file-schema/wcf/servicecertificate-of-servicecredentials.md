---
title: "&lt;serviceCredentials&gt; 的 &lt;serviceCertificate&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 597ae6d5-4938-4950-9f5e-b2280e816182
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;serviceCredentials&gt; 的 &lt;serviceCertificate&gt;
指定一个 X.509 证书，以供服务用来向使用 Message 安全模式的客户端证明自己的身份。  
  
## 语法  
  
```  
  
<serviceCertificate findValue="String"   
    storeLocation="LocalMachine/CurrentUser"  
    storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"  
X509FindType="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"  
/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`findValue`|一个字符串，包含要在 X.509 证书存储中搜索的值。  此属性中包含的类型必须满足指定 X509FindType 的要求。  默认值为一个空字符串。|  
|`storeLocation`|指定客户端可用于验证服务器证书的 X.509 证书存储的位置。  包括以下有效值：<br /><br /> -   LocalMachine：分配给本地计算机的证书存储。<br />-   CurrentUser：分配给当前用户的证书存储。<br /><br /> 默认值为 LocalMachine。|  
|`storeName`|指定要打开的 X.509 证书存储区的名称。  包括以下有效值：<br /><br /> -   AddressBook：其他用户的证书存储。<br />-   AuthRoot：第三方证书颁发机构 \(CA\) 的证书存储。<br />-   CertificatAuthority：中间证书颁发机构 \(CA\) 的证书存储。<br />-   Disallowed：吊销的证书的证书存储。<br />-   My：个人证书的证书存储。<br />-   Root：受信任的根证书颁发机构 \(CA\) 的证书存储。<br />-   TrustedPeople：直接受信任的人和资源的证书存储。<br />-   TrustedPublisher：直接受信任的发行者的证书存储。<br /><br /> 默认值为 My。|  
|`X509FindType`|定义要执行的 X.509 搜索的类型。  包括以下有效值：<br /><br /> -   FindByThumbprint<br />-   FindBySubjectName<br />-   FindBySubjectDistinguishedName<br />-   FindByIssuerName<br />-   FindByIssuerDistinguishedName<br />-   FindBySerialNumber<br />-   FindByTimeValid<br />-   FindByTimeNotYetValid<br />-   FindByTemplateName<br />-   FindByApplicationPolicy<br />-   FindByCertificatePolicy<br />-   FindByExtension<br />-   FindByKeyUsage<br />-   FindBySubjectKeyIdentifier<br /><br /> `findValue` 属性中包含的类型必须满足指定 X509FindType 的要求。<br /><br /> 默认值为 FindBySubjectDistinguishedName。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<serviceCredentials\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)|指定要用于对服务进行身份验证的凭据以及与客户端凭据验证相关的设置。|  
  
## 备注  
 使用此元素可指定一个 X.509 证书，以供服务用来向使用 Message 安全模式的客户端证明自己的身份。  如果您使用的是将会定期续订的证书，则证书的指纹将会变更。  在此情况下，请使用主题名称作为 `X509FindType`，因为可以使用同一主题名称来重新颁发该证书。  
  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)]使用此元素的更多信息，请参见[如何：指定客户端凭据值](../../../../../docs/framework/wcf/how-to-specify-client-credential-values.md)。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.X509RecipientCertificateServiceElement>   
 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.ServiceCertificate%2A>   
 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential>   
 <xref:System.ServiceModel.Description.ServiceCredentials.ServiceCertificate%2A>   
 [如何：指定客户端凭据值](../../../../../docs/framework/wcf/how-to-specify-client-credential-values.md)   
 [安全行为](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)