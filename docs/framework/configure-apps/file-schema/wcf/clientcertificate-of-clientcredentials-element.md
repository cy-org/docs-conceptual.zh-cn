---
title: "&lt;clientCredentials&gt; 的 &lt;clientCertificate&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3b3fa000-3434-4142-a178-11903bdd2c5d
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;clientCredentials&gt; 的 &lt;clientCertificate&gt; 元素
定义用于向服务验证客户端身份的 X.509 证书。  
  
## 语法  
  
```  
  
<clientCertificate findValue="String"   
    storeLocation="LocalMachine/CurrentUser"  
    storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"  
X509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"  
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`findValue`|一个字符串，包含要在 X.509 证书存储中搜索的值。  此属性中包含的类型必须满足 `X509FindType` 属性值的要求。  默认值为一个空字符串。|  
|`storeLocation`|指定客户端用于向服务验证自身身份的 X.509 证书的位置。  包括以下有效值：<br /><br /> -   LocalMachine：分配给本地计算机的证书存储。<br />-   CurrentUser：分配给当前用户的证书存储。<br /><br /> 默认值为 LocalMachine。  此属性的类型为 <xref:System.Security.Cryptography.X509Certificates.StoreLocation>。|  
|`storeName`|指定要搜索的 X.509 证书存储的名称。  包括以下有效值：<br /><br /> -   AddressBook：其他用户的证书存储。<br />-   AuthRoot：第三方证书颁发机构 \(CA\) 的证书存储。<br />-   CertificateAuthority：中间证书颁发机构 \(CA\) 的证书存储。<br />-   Disallowed：吊销的证书的证书存储。<br />-   My：个人证书的证书存储。<br />-   Root：受信任的根证书颁发机构 \(CA\) 的证书存储。<br />-   TrustedPeople：直接受信任的人和资源的证书存储。<br />-   TrustedPublisher：直接受信任的发行者的证书存储。<br /><br /> 默认值为 My。  此属性的类型为 <xref:System.Security.Cryptography.X509Certificates.StoreName>。|  
|X509FindType|定义要执行的 X.509 搜索的类型。  `findValue` 属性中包含的类型必须满足此属性的要求。  包括以下有效值：<br /><br /> -   FindByThumbPrint<br />-   FindBySubjectName<br />-   FindBySubjectDistinguishedName<br />-   FindByIssuerName<br />-   FindByIssuerDistinguishedName<br />-   FindBySerialNumber<br />-   FindByTimeValid<br />-   FindByTimeNotYetValid<br />-   FindByTemplateName<br />-   FindByApplicationPolicy<br />-   FindByCertificatePolicy<br />-   FindByExtension<br />-   FindByKeyUsage<br />-   FindBySubjectKeyIdentifier<br /><br /> 默认值为 FindBySubjectDistinguishedName。  此属性的类型为 <xref:System.Security.Cryptography.X509Certificates.X509FindType>。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<clientCredentials\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|指定用于向服务验证客户端身份的凭据。|  
  
## 备注  
 此配置元素指定用于对具有此元素的客户端进行身份验证的证书。  [!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [如何：指定客户端凭据值](../../../../../docs/framework/wcf/how-to-specify-client-credential-values.md).  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement.ClientCertificate%2A>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Description.ClientCredentials.ClientCertificate%2A>   
 <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement>   
 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>   
 [安全行为](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [如何：指定客户端凭据值](../../../../../docs/framework/wcf/how-to-specify-client-credential-values.md)   
 [保证客户端的安全](../../../../../docs/framework/wcf/securing-clients.md)   
 [使用证书](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)