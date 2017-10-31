---
title: "&lt;certificate&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9b3d9233-ef35-477a-bf5d-efd1e80a52f4
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# &lt;certificate&gt; 元素
指定要用于为对等客户端的消息进行签名和加密的 X.509 证书。  
  
## 语法  
  
```  
  
<certificate findValue="String"   
  
storeLocation="LocalMachine/CurrentUser"  
      storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"  
      X509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"  
/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`findValue`|一个字符串，包含要在 X.509 证书存储中搜索的值。  此属性中包含的类型必须满足指定 `x509FindType` 的要求。  默认值为一个空字符串。|  
|`storeLocation`|指定客户端可用于验证对等方的证书的 X.509 证书存储的位置。  包括以下有效值：<br /><br /> -   LocalMachine：分配给本地计算机的证书存储。<br />-   CurrentUser：分配给当前用户的证书存储。<br /><br /> 默认值为 LocalMachine。|  
|`storeName`|指定要打开的 X.509 证书存储区的名称。  包括以下有效值：<br /><br /> -   AddressBook：其他用户的证书存储。<br />-   AuthRoot：第三方证书颁发机构 \(CA\) 的证书存储。<br />-   CertificateAuthority：中间证书颁发机构 \(CA\) 的证书存储。<br />-   Disallowed：吊销的证书的证书存储。<br />-   My：个人证书的证书存储。<br />-   Root：受信任的根证书颁发机构 \(CA\) 的证书存储。<br />-   TrustedPeople：直接受信任的人和资源的证书存储。<br />-   TrustedPublisher：直接受信任的发行者的证书存储。<br /><br /> 默认值为 My。|  
|`X509FindType`|定义要执行的 X.509 搜索的类型。  包括以下有效值：<br /><br /> -   FindByThumbPrint<br />-   FindBySubjectName<br />-   FindBySubjectDistinguishedName<br />-   FindByIssuerName<br />-   FindByIssuerDistinguishedName<br />-   FindBySerialNumber<br />-   FindByTimeValid<br />-   FindByTimeNotYetValid<br />-   FindByTemplateName<br />-   FindByApplicationPolicy<br />-   FindByCertificatePolicy<br />-   FindByExtension<br />-   FindByKeyUsage<br />-   FindBySubjectKeyIdentifier<br /><br /> `findValue` 属性中包含的类型必须满足指定 `X509FindType` 的要求。<br /><br /> 默认值为 FindBySubjectDistinguishedName。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<peer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/peer-of-clientcredentials-element.md)|指定在向对等客户端进行身份验证时使用的凭据。|  
  
## 备注  
 此配置元素包含对对等网格中的邻居进行身份验证时使用的 X509Certificate2 实例。  
  
 有关对等编程的更多信息，请参见[对等网络](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)。  
  
## 示例  
 下面的代码指定如何查找在对等方案中使用的证书。  
  
```  
<behaviors>  
 <endpointBehaviors>  
  <behavior name="MyEndpointBehavior">  
   <clientCredentials>  
    <peer>  
     <certificate findValue="www.contoso.com"   
                   storeLocation="LocalMachine"  
                   x509FindType="FindByIssuerName" />  
    </peer>  
   </clientCredentials>  
  </behavior>  
</endpointBehaviors>  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.PeerCredentialElement>   
 <xref:System.ServiceModel.Configuration.PeerCredentialElement.Certificate%2A>   
 <xref:System.ServiceModel.Configuration.X509PeerCertificateElement>   
 <xref:System.ServiceModel.Security.PeerCredential.Certificate%2A>   
 [使用证书](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [对等网络](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)   
 [Peer Channel Message Authentication](http://msdn.microsoft.com/zh-cn/80e73386-514e-4c30-9e4a-b9ca8c173a95)   
 [Peer Channel Custom Authentication](http://msdn.microsoft.com/zh-cn/4aa8a82e-41a8-48e2-8621-7e1cbabdca7c)   
 [保护对等通道应用程序](../../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md)