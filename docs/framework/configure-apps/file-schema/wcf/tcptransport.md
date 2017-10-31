---
title: "&lt;tcpTransport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 8fcd18c1-9958-42e7-b442-7903f7bdb563
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;tcpTransport&gt;
定义通道用于传输自定义绑定消息的 TCP 传输。  
  
## 语法  
  
```  
  
<tcpTransport   
    listenBacklog="Integer"  
        portSharingEnabled="Boolean"  
    teredoEnabled="Boolean"  
    transferMode=”Buffered/Streamed”  
        <connectionPoolSettings  
          groupName=”String”  
        idleTimeout"TimeSpan"  
        leaseTimeout="TimeSpan"  
        maxOutboundConnectionsPerEndpopint=”Integer” />  
/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|channelInitializationTimeout|通道在断开连接前可处于初始化状态的最长时间（秒）。  此配额包括 TCP 连接可用于使用 .Net Message Framing 协议对自身进行身份验证的时间。  客户端需要发送一些初始数据，然后服务器才有足够的信息来执行身份验证。  默认值为 30 秒。|  
|listenBacklog|可为 Web 服务挂起的最大排队连接请求数。  `connectionLeaseTimeout` 属性限制客户端在引发连接异常之前将等待连接的持续时间。  这是一个套接字级别属性，控制可能为 Web 服务挂起的最大排队连接请求数。  ListenBacklog 太低时，WCF 将停止接受请求并因此删除新连接，直到服务器确认一些现有队列连接。默认值为 16 \* 处理器数。|  
|portSharingEnabled|一个布尔值，指定是否为此连接启用 TCP 端口共享。  如果此值为 `false`，则每个绑定都将使用自己的独占端口。  默认值为 `false`。<br /><br /> 此设置只与服务相关。  客户端并不会受影响。<br /><br /> 使用此设置要求通过将 Windows Communication Foundation \(WCF\) TCP 端口共享服务的“启动类型”设置为“手动”或“自动”来启用该服务。|  
|teredoEnabled|一个布尔值，指定是否启用 Teredo（一种用于对防火墙后的客户端进行寻址的技术）。  默认值为 `false`。<br /><br /> 此属性为基础 TCP 套接字启用 Teredo。  有关更多信息，请参见 [Teredo 概述](http://go.microsoft.com/fwlink/?LinkId=95339)（可能为英文网页）。<br /><br /> 此属性仅适用于 [!INCLUDE[wxpsp2](../../../../../includes/wxpsp2-md.md)] 和 [!INCLUDE[ws2003](../../../../../includes/ws2003-md.md)]。  [!INCLUDE[wv](../../../../../includes/wv-md.md)] 具有用于 Teredo 的计算机范围的配置选项，因此运行 Vista 时将忽略此属性。  Teredo 要求客户端和服务计算机都安装 Microsoft IPv6 堆栈，并进行正确的配置以便使用 Teredo。  有关配置 Teredo 的更多信息，请参见 [Teredo 概述](http://go.microsoft.com/fwlink/?LinkId=95339)（可能为英文网页）。  有关更多信息，请参见 [Windows Server 2003 技术中心](http://go.microsoft.com/fwlink/?LinkId=49888)（可能为英文网页）。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<绑定\>](../../../../../docs/framework/misc/binding.md)|定义自定义绑定的所有绑定功能。|  
  
## 备注  
 此传输使用“net.tcp:\/\/hostname:port\/path”形式的 URI。  其他 URI 组件是可选的。  
  
 `tcpTransport` 元素是创建实现 TCP 传输协议的自定义绑定的起始点。  针对 WCF 到 WCF 的通信对此传输进行了优化。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.TcpTransportElement>   
 <xref:System.ServiceModel.Channels.TcpTransportBindingElement>   
 <xref:System.ServiceModel.Channels.TransportBindingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [传输](../../../../../docs/framework/wcf/feature-details/transports.md)   
 [选择传输方式](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [扩展绑定](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [自定义绑定](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)