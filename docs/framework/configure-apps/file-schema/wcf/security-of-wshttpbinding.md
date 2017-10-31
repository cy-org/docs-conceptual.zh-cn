---
title: "&lt;wsHttpBinding&gt; 的 &lt;security&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8658b162-2ddf-4162-a869-aa517a42288a
caps.latest.revision: 18
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 18
---
# &lt;wsHttpBinding&gt; 的 &lt;security&gt;
表示 [\<wsHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)的安全功能。  
  
## 语法  
  
```  
  
<security mode="Message/None/Transport/TransportWithMessageCredential">  
   <transport  
         clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"  
      proxyCredentialType="Basic/Digest/None/Ntlm/Windows"  
      realm="string"   
      defaultClientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"  
      defaultProxyCredentialType="Basic/Digest/None/Ntlm/Windows"  
      defaultRealm="string" />  
   <message  
            clientCredentialType="Certificate/IssuedToken/None/UserName/Windows"  
      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
       establishSecurityContext="Boolean"   
      negotiateServiceCredential="Boolean"/>  
</security>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|mode|-   可选。  指定所应用的安全类型。  默认值为 `Message`。<br />-   此属性的类型为 <xref:System.ServiceModel.SecurityMode>。|  
  
## Mode 属性  
  
|值|描述|  
|-------|--------|  
|无|禁用安全性。|  
|传输|使用 HTTPS 提供安全性。  此服务需要使用 SSL 证书进行配置。  消息使用 HTTPS 得到了全面保护，客户端使用服务的 SSL 证书对消息进行身份验证。  客户端身份验证通过  [\<传输\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-wshttpbinding.md)的 `ClientCredentials` 特性进行控制。|  
|消息|使用 SOAP 消息安全提供安全性。  默认情况下，将对 SOAP 正文进行加密和签名。  此模式提供了各种各样的功能，例如服务凭据在带外客户端是否可用、要使用的算法组以及通过 Security.Message 属性要应用于消息正文的保护级别。  每个会话将执行一次客户端身份验证，身份验证的结果在会话过程中将被缓存。|  
|TransportWithMessageCredential|在此模式下，HTTPS 将提供完整性、保密性和服务器身份验证，SOAP 消息安全将提供客户端身份验证。  默认情况下，每个会话将执行一次客户端身份验证，身份验证的结果在会话过程中将被缓存。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<传输\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-wshttpbinding.md)|定义传输安全设置。  此元素与 <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement> 类型相对应。|  
|[\<消息\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md)|定义消息的安全设置。  此元素与 <xref:System.ServiceModel.Configuration.MessageSecurityOverHttpElement> 类型相对应。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<wsHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)|HTTP 传输应用程序的安全绑定。|  
  
## 备注  
 WSHttpBinding 类专用于与实现 WS\-\* 规范的服务进行互操作。  此绑定的传输安全为 HTTP 上的安全套接字层 \(SSL\)，即 HTTPS。  
  
## 请参阅  
 <xref:System.ServiceModel.WSHttpSecurity>   
 <xref:System.ServiceModel.WSHttpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpBindingElement.Security%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpSecurityElement>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)