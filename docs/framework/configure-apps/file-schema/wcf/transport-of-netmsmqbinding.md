---
title: "&lt;netMsmqBinding&gt; 的 &lt;transport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 72e1b338-39f0-4af1-a5d9-7a2fb79f6a0b
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;netMsmqBinding&gt; 的 &lt;transport&gt;
定义传输安全设置。  
  
## 语法  
  
```  
  
<netMsmqBinding>  
    <binding>  
    <security>  
         <transport msmqAuthenticationMode="None/WindowsDomain/Certificate"  
            msmqEncryptionAlgorithm="RC4Stream/AES"  
            msmqProtectionLevel="None/Sign/EncryptAndSign"  
            msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />  
    </security>  
   </binding>  
</netMsmqBinding>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|msmqAuthenticationMode|指定 MSMQ 传输必须采用什么方式对消息进行身份验证。  包括以下有效值：<br /><br /> -   None：不进行身份验证。<br />-   WindowsDomain：身份验证机制使用 Active Directory 检索与消息关联的安全标识符的 X.509 证书。  然后使用它来检查队列的 ACL 以确保用户具有队列写权限。<br />-   Certificate：通道从证书存储中检索证书。<br /><br /> 默认值为 `WindowsDomain`。<br /><br /> 如果将此属性设置为 `None`，则 `msmqProtectionLevel` 属性也必须设置为 `None`。  此特性的类型为 <xref:System.ServiceModel.MsmqAuthenticationMode>|  
|msmqEncryptionAlgorithm|指定在消息队列管理器之间传输消息时用于在网络上对消息进行加密的算法。  包括以下有效值：<br /><br /> -   RC4Stream<br />-   AES<br />-   默认值为 `RC4Stream`。  此属性的类型为 <xref:System.ServiceModel.MsmqEncryptionAlgorithm>。|  
|msmqProtectionLevel|指定在 MSMQ 传输级别采用什么方式来保护消息。  加密可确保消息的完整性，而签名和加密不仅可以确保消息的完整性，还可以确保消息的不可否认性。  也就是说，消息确实来自发送者，发送者与他所声称的身份一致。  包括以下有效值：<br /><br /> -   None：无保护。<br />-   Sign：对消息进行签名。<br />-   EncryptAndSign：对消息进行加密和签名。<br />-   默认值为 `Sign`。|  
|msmqSecureHashAlgorithm|指定用于计算消息摘要的哈希算法。  包括以下有效值：<br /><br /> -   MD5<br />-   SHA1<br />-   SHA256<br />-   SHA512<br /><br /> 默认值为 `SHA1`。  此属性的类型为 <xref:System.ServiceModel.MsmqSecureHashAlgorithm>。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<安全性\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-netmsmqbinding.md)|定义排队传输的传输安全设置。|  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>   
 <xref:System.ServiceModel.Configuration.NetMsmqSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.NetMsmqSecurity.Transport%2A>   
 <xref:System.ServiceModel.MsmqTransportSecurity>   
 [WCF 中的队列](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)