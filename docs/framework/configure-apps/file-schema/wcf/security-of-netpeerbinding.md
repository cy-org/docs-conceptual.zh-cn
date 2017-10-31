---
title: "&lt;netPeerBinding&gt; 的 &lt;security&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1ef40d8c-f903-4426-9b08-da81462766d8
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# &lt;netPeerBinding&gt; 的 &lt;security&gt;
定义 [\<netPeerTcpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/netpeertcpbinding.md) 的安全设置，包括使用的身份验证类型和用于消息传输的安全性。  
  
## 语法  
  
```  
  
<netPeerBinding>  
    <binding>  
        <security mode="Message/None/Transport//TransportWithMessageCredential">  
            <transport credentialType="Certificate/Password" />  
        </security>  
    </binding>  
</netPeerBinding>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|mode|可选。  指定采用此绑定配置的对等端所使用的安全类型。  默认值为 `Message`。  此属性的类型为 <xref:System.ServiceModel.SecurityMode>。|  
  
## mode 属性  
  
|值|描述|  
|-------|--------|  
|消息|SOAP 安全提供身份验证、完整性和保密性。|  
|无|禁用安全性。|  
|传输|使用 HTTPS 提供安全性。|  
|TransportWithMessageCredential|HTTPS 提供身份验证和保密性。  SOAP 消息提供丰富的凭据类型。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<传输\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-netpeertcpbinding.md)|定义采用此绑定配置的对等端所发送的安全消息的传输类型。  此元素的类型为 <xref:System.ServiceModel.Configuration.PeerTransportSecurityElement>。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<绑定\>](../../../../../docs/framework/misc/binding.md)|定义 [\<netPeerTcpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/netpeertcpbinding.md)的所有绑定功能。|  
  
## 备注  
 安全性可以是特定于消息的，也可以是特定于传输的。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.PeerSecurityElement>   
 <xref:System.ServiceModel.NetPeerTcpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.NetPeerTcpBindingElement.Security%2A>   
 <xref:System.ServiceModel.PeerSecuritySettings>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [选择凭据类型](../../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)