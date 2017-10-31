---
title: "&lt;peerTransport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1a5013a-9dd4-4a27-b114-795b8b323177
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# &lt;peerTransport&gt;
定义自定义绑定的对等传输。  
  
## 语法  
  
```  
  
<peerTransport   
    listenIpAddress="String"  
    maxBufferPoolSize="Integer"  
    maxReceivedMessageSize="Integer"  
    port="Integer"  
        <security>  
    </security>  
/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|listenIpAddress|一个字符串，指定对等节点将在其上侦听 TCP 消息的 IP 地址。  默认值为 `null`。|  
|maxBufferPoolSize|一个正整数，指定缓冲池的最大大小。  默认值为 524288。<br /><br /> WCF 的许多组件使用缓冲区。  每次使用缓冲区时，创建和销毁它们都将占用大量资源，而缓冲区的垃圾回收过程也是如此。  利用缓冲池，可以从缓冲池中获得缓冲区，使用缓冲区，然后在完成工作后将其返回给缓冲池。  这样就避免了创建和销毁缓冲区的系统开销。|  
|maxReceivedMessageSize|一个正整数，定义包括标头在内的最大消息大小（以字节为单位）。  如果消息对于接收方而言太大，则消息发送方将收到 SOAP 错误。  接收方将删除该消息，并在跟踪日志中创建事件项。  默认值为 65536。|  
|端口|一个整数，指定此绑定将用于处理对等通道 TCP 消息的网络接口端口。  该值必须介于 <xref:System.Net.IPEndPoint.MinPort> 和 <xref:System.Net.IPEndPoint.MaxPort> 之间。  默认值为 0。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<安全性\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-peertransport.md)|定义此传输的安全设置。  此元素的类型为 <xref:System.ServiceModel.Configuration.PeerSecurityElement>。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<绑定\>](../../../../../docs/framework/misc/binding.md)|定义自定义绑定的所有绑定功能。|  
  
## 备注  
 此传输不可用于包含请求\/答复操作的协定。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.PeerTransportElement>   
 <xref:System.ServiceModel.Channels.PeerTransportBindingElement>   
 <xref:System.ServiceModel.Channels.TransportBindingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [传输](../../../../../docs/framework/wcf/feature-details/transports.md)   
 [选择传输方式](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [扩展绑定](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [自定义绑定](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)