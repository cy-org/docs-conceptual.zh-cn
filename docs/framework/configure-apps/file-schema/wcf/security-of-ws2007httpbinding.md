---
title: "&lt;ws2007HttpBinding&gt; 的 &lt;security&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fdda0ff7-b462-4e26-af52-e87ddab71945
caps.latest.revision: 10
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 10
---
# &lt;ws2007HttpBinding&gt; 的 &lt;security&gt;
表示与 [\<ws2007HttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md) 元素配合使用的安全设置。  
  
## 语法  
  
```  
  
<system.serviceModel>  
    <bindings>  
        <ws2007HttpBinding>  
            <binding name = "string">  
              <security mode="None/Message/Transport/TransportWithMessageCredential">  
                  <transport>  
                  </transport>  
                  <message>  
                  </message>  
              </security  
        </ws2007HttpBinding>  
    </bindings>  
</system.ServiceModel>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`mode`|-   可选。  指定所应用的安全类型。  默认值为 `Message`。<br /><br /> 此属性的类型为 <xref:System.ServiceModel.SecurityMode>。|  
  
## Mode 属性  
  
|值|描述|  
|-------|--------|  
|`None`|禁用安全性。|  
|`Transport`|使用 HTTPS 提供安全性。  此服务必须使用安全套接字层 \(SSL\) 证书进行配置。  消息使用 HTTPS 获得全面保护，而且客户端使用服务的 SSL 证书对服务进行身份验证。  客户端身份验证是通过 [\<传输\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-ws2007httpbinding.md) 元素的 `ClientCredentials` 属性控制的。|  
|`Message`|使用 SOAP 消息安全提供安全性。  默认情况下，将对 SOAP 正文进行加密和签名。  此模式提供了各种各样的功能，例如服务凭据在带外客户端是否可用、要使用的算法组以及通过 <xref:System.ServiceModel.Security.SecurityMessageProperty> 要应用于消息正文的保护级别。  每个会话将执行一次客户端身份验证，身份验证的结果在会话过程中将进行缓存。|  
|`TransportWithMessageCredential`|在此模式下，HTTPS 将提供完整性、保密性和服务器身份验证，SOAP 消息安全将提供客户端身份验证。  默认情况下，每个会话将执行一次客户端身份验证，身份验证的结果在会话过程中将进行缓存。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<传输\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-ws2007httpbinding.md)|定义传输安全设置。  此元素与 <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement> 类型相对应。  仅在将模式设置为“Transport”时才应用这些设置。|  
|[\<消息\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-ws2007httpbinding.md)|定义消息的安全设置。  此元素与 <xref:System.ServiceModel.Configuration.MessageSecurityOverHttpElement> 类型相对应。  将模式设置为“Transport”时，不应用这些设置。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<ws2007HttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md)|HTTP 传输应用程序的安全绑定。|  
  
## 备注  
 此元素专用于与实现 WS\-\* 规范的服务进行互操作。  此绑定的传输安全为 HTTP 上的安全套接字层 \(SSL\)，即 HTTPS。  
  
## 请参阅  
 <xref:System.ServiceModel.WSHttpSecurity>   
 <xref:System.ServiceModel.WSHttpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpBindingElement.Security%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpSecurityElement>   
 <xref:System.ServiceModel.BasicHttpSecurity>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)