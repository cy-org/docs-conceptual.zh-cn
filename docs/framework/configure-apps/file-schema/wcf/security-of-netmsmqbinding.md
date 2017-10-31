---
title: "&lt; netMsmqBinding&gt; 的 &lt;security&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 001d11a9-7439-498c-b09d-fca20eaf8cd3
caps.latest.revision: 15
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 15
---
# &lt; netMsmqBinding&gt; 的 &lt;security&gt;
定义 MSMQ 绑定的安全设置。  它指定是否启用传输或 SOAP 安全；如果启用，还指定所使用的身份验证模式和保护级别。  
  
## 语法  
  
```  
  
<security mode="None/Transport/Message/Both">  
   <transport msmqAuthenticationMode="None/WindowsDomain/Certificate"  
      msmqEncryptionAlgorithm="RC4Stream/AES"  
      msmqProtectionLevel="None/Sign/EncryptAndSign"  
      msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />  
      <message  
      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
      clientCredentialType="None/Windows/UserName/Certificate/CardSpace"/>  
</security>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|mode|指定用于控制完整性、保密性和身份验证的安全类型。  包括以下有效值：<br /><br /> -   None：禁用安全性。<br />-   Transport：通过传输来提供保护和身份验证。  这适用于两个队列管理器之间的消息安全性。  未在应用程序和队列管理器之间提供安全性。  现有的 Msmq 应用程序与此类型的安全模式功能等效。<br />-   Message：指定端与端之间的应用程序安全性。  未在传输层提供安全性。  这类似于其他标准绑定提供的安全性。<br />-   Both：在传输层和 SOAP 消息层提供安全性。  在这两个层上需要相同的凭据。<br /><br /> 默认值为 Transport。  此属性的类型为 <xref:System.ServiceModel.NetMsmqSecurityMode>。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<消息\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-netmsmqbinding.md)|定义 SOAP 消息安全设置。  此元素的类型为 <xref:System.ServiceModel.Configuration.MessageSecurityOverMsmqElement>。|  
|[\<传输\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-netmsmqbinding.md)|定义 MSMQ 传输的安全设置。  此元素的类型为 <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|绑定|[\<netMsmqBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md) 的绑定元素|  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.NetMsmqSecurityElement>   
 <xref:System.ServiceModel.NetMsmqBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.NetMsmqBindingElement.Security%2A>   
 <xref:System.ServiceModel.NetMsmqSecurity>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)   
 [WCF 中的队列](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)