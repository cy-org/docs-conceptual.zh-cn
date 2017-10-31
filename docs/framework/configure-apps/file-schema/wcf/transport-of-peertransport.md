---
title: "&lt;peerTransport&gt; 的 &lt;transport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d7116240-845c-4b6f-b203-262de6b597ef
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;peerTransport&gt; 的 &lt;transport&gt;
指定采用此绑定配置的对等方所发送的安全消息的传输类型。  
  
## 语法  
  
```  
  
<security>  
   <transport credentialType="Certificate/Password" />  
</security>         
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|credentialType|可选。  指定用于验证通过对等传输发送的消息的凭据的类型。  此属性的类型为 <xref:System.ServiceModel.PeerTransportCredentialType>。|  
  
## credentialType 属性  
  
|值|描述|  
|-------|--------|  
|证书|对等通道传输的身份验证需要 X509 证书。|  
|密码|对等通道传输的身份验证需要正确的密码。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<安全性\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-peertransport.md)|定义对等传输的安全设置。|  
  
## 备注  
 仅当 [\<安全性\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-peertransport.md) 的模式属性设置为 `Transport` 或 `TransportWithMessageCredential` 时才设置此元素。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.PeerTransportSecurityElement>   
 <xref:System.ServiceModel.PeerSecuritySettings.Transport%2A>   
 <xref:System.ServiceModel.PeerTransportSecuritySettings>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [传输安全](../../../../../docs/framework/wcf/feature-details/transport-security.md)   
 [传输](../../../../../docs/framework/wcf/feature-details/transports.md)   
 [选择传输方式](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [扩展绑定](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [自定义绑定](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)