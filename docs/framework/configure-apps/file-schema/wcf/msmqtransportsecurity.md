---
title: "&lt;msmqTransportSecurity&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 092e911b-ab1b-4069-a26e-6134c3299e06
caps.latest.revision: 10
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 10
---
# &lt;msmqTransportSecurity&gt;
指定自定义绑定的 MSMQ 传输的安全设置。  
  
## 语法  
  
```  
  
<msmqTransportSecurity>  
   msmqAuthenticationMode="None/Windows/Certificate"  
   msmqEncryptionAlgorithm="RC4Stream/AES"  
   msmqProtectionLevel="None/Sign/EncryptAndSign"  
   msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />  
</msmqTransportSecurity>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`msmqAuthenticationMode`|指定 MSMQ 传输必须采用什么方式对消息进行身份验证。  如果将此属性设置为 `None`，则 `msmqProtectionLevel` 属性的值也必须设置为 `None`。<br /><br /> 包括以下有效值：<br /><br /> -   None：不进行身份验证。<br />-   Windows：身份验证机制使用 Active Directory 获取与消息关联的 SID 的 X.509 证书。  然后使用它来检查队列的 ACL 以确保用户有权写入队列。<br />-   Certificate：通道从证书存储中获得证书。<br /><br /> 默认值为 Windows。  此属性的类型为 <xref:System.ServiceModel.MsmqAuthenticationMode>。|  
|`msmqEncryptionAlgorithm`|指定在消息队列管理器之间传输消息时用于在网络上对消息进行加密的算法。  包括以下有效值：<br /><br /> -   RC4Stream<br />-   AES<br /><br /> 默认值为 RC4Stream。  此属性的类型为 <xref:System.ServiceModel.MsmqEncryptionAlgorithm>。|  
|`msmqProtectionLevel`|指定在 MSMQ 传输级别采用什么方式来保护消息。  加密可以确保消息的完整性，而 EncryptAndSign 不仅可以确保消息的完整性，还可以确保消息的不可否认性，也就是说，消息确实来自发送者，并且发送者与其所声称的身份一致。  包括以下有效值：<br /><br /> -   None：无保护。<br />-   Sign：对消息进行签名。<br />-   EncryptAndSign：对消息进行加密和签名。<br /><br /> 默认值为 Sign。  此属性的类型为 <xref:System.Net.Security.ProtectionLevel>。|  
|`msmqSecureHashAlgorithm`|指定用于计算签名中的摘要的算法。  包括以下有效值：<br /><br /> -   MD5<br />-   SHA1<br />-   SHA256<br />-   SHA512<br /><br /> 默认值为 SHA1。  此属性的类型为 <xref:System.ServiceModel.MsmqSecureHashAlgorithm>。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<msmqIntegration\>](../../../../../docs/framework/configure-apps/file-schema/wcf/msmqintegration.md)|指定与消息队列 \(MSMQ\) 发送方或接收方进行交互所需的设置。|  
|[\<msmqTransport\>](../../../../../docs/framework/configure-apps/file-schema/wcf/msmqtransport.md)|指定使用本机 MSMQ 协议的 Windows Communication Foundation \(WCF\) 服务的队列通信属性。|  
  
## 备注  
 有关传输安全性的更多信息，请参见[传输安全](../../../../../docs/framework/wcf/feature-details/transport-security.md)。  
  
## 请参阅  
 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurity>   
 <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [WCF 中的队列](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [传输](../../../../../docs/framework/wcf/feature-details/transports.md)   
 [选择传输方式](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [扩展绑定](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [自定义绑定](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [传输安全](../../../../../docs/framework/wcf/feature-details/transport-security.md)