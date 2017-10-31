---
title: "&lt;netTcpBinding&gt; 的 &lt;security&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 286cd191-4fd5-4c4e-a223-9c71cf7fdead
caps.latest.revision: 18
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 18
---
# &lt;netTcpBinding&gt; 的 &lt;security&gt;
定义绑定的安全设置。  
  
## 语法  
  
```  
  
<security mode="Message/None/Transport/TransportWithCredential">  
   <transport  
      clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"  
           protectionLevel="None/Sign/EncryptAndSign" />  
   <message  
      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
      clientCredentialType="Certificate/IssuedToken/None/UserName/Windows" />  
</security>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|mode|可选。  指定所应用的安全类型。  以下列出了有效值。  默认值为 `Transport`。<br /><br /> 此属性的类型为 <xref:System.ServiceModel.SecurityMode>。|  
  
## mode 属性  
  
|值|描述|  
|-------|--------|  
|无|禁用安全性。|  
|传输|使用 TLS over TCP 或 SPNego 提供传输安全性。  此服务可能需要使用 SSL 证书进行配置。  可以通过此模式来控制保护级别。|  
|消息|使用 SOAP 消息安全提供安全性。  默认情况下，将对 SOAP 正文进行加密和签名。  此模式提供了各种各样的功能，例如服务凭据在带外客户端是否可用、要使用的算法组以及要应用于消息正文的保护级别。  每个会话将执行一次客户端身份验证，身份验证的结果在会话过程中将被缓存。|  
|TransportWithMessageCredential|传输安全性与消息安全性结合使用。  使用 TLS over TCP 或 SPNego 提供传输安全性，传输安全性可确保完整性、保密性和服务器身份验证。  SOAP 消息安全性提供客户端身份验证。  默认情况下，每个会话将执行一次客户端身份验证，身份验证的结果在会话过程中将被缓存。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<transport\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-nettcpbinding.md)|定义传输的安全设置。  此元素的类型为 <xref:System.ServiceModel.Configuration.TcpTransportSecurityElement>。|  
|[\<消息\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-element-of-nettcpbinding.md)|定义消息的安全设置。  此元素的类型为 <xref:System.ServiceModel.Configuration.MessageSecurityOverTcpElement>。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|绑定|[\<netTcpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)的绑定元素。|  
  
## 备注  
 每个标准绑定都提供用于控制传输安全性要求的参数。  这些参数通常包括指定是使用消息级安全性还是使用传输级安全性的安全模式，还包括客户端凭据类型的选项。  基于这些参数提供的可供选择的选项，构建一个具有适当安全性的信道堆栈。  
  
 由 Windows Communication Foundation \(WCF\) 提供的系统提供的绑定是一组旨在满足一些最常见的方案要求的绑定。  所有这些绑定都允许为某些特定的目标方案指定安全要求。  
  
 此配置元素提供用于 `netTcpBinding` 的安全规范。  这是一种适合于跨计算机通信的安全、可靠且进行了优化的绑定。  默认情况下，它生成运行时通信堆栈，该堆栈支持用于消息传递的 TCP、消息安全性和身份验证的 Windows 安全、可靠的 WS\-ReliableMessaging，以及二进制消息编码。  
  
## 请参阅  
 <xref:System.ServiceModel.NetTcpSecurity>   
 <xref:System.ServiceModel.NetTcpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.NetTcpBindingElement.Security%2A>   
 <xref:System.ServiceModel.Configuration.NetTcpSecurityElement>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)