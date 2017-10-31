---
title: "&lt;udpTransportSettings&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 842d92e9-6199-4ec5-b2d1-58533054e1f0
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;udpTransportSettings&gt;
此配置元素公开 [\<udpDiscoveryEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/udpdiscoveryendpoint.md) 的 UDP 传输设置。  
  
## 语法  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <udpDiscoveryEndpoint>   
          <standardEndpoint>  
               <updTransportSettings>  
                  duplicateMessageHistoryLength=”Integer”  
                  maxBufferPoolSize=”Integer”   
                  maxMulticastRetransmitCount=”Integer”  
                  maxPendingMessageCount=”Integer”  
                  maxReceivedMessageSize=”Integer”  
                  maxUnicastRetransmitCount=”Integer”  
                  multicastInterfaceId=”String”  
                  socketReceiveBufferSize=”Integer”  
                  timeToLive=”Integer” />   
          </standardEndpoint>  
       </udpDiscoveryEndpoint>          
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|duplicateMessageHistoryLength|一个整数，指定传输用于标识重复消息的最大消息哈希数。  将在 TransportManager 级别进行重复检测。  将此属性设置为 0 即可禁用重复检测。<br /><br /> 系统管理员或开发人员可以使用此特性关闭重复消息检测算法。  如果您希望实现自己的重复检测算法，可能需要这一功能。<br /><br /> 默认值为 4112。|  
|maxBufferPoolSize|一个整数，指定传输使用的任何缓冲池的最大大小。|  
|maxMulticastRetransmitCount|一个整数，指定应重新传输消息的最大次数（包括第一次发送）。<br /><br /> 默认值为 2。|  
|maxPendingMessageCount|一个整数，指定已经接收但尚未从单个通道实例的 InputQueue 中移除的最大消息数。  如果 InputQueue 已达到挂起消息计数上限，则将丢弃消息。<br /><br /> 默认值为 32。|  
|maxReceivedMessageSize|一个整数，指定绑定可处理的消息的最大大小。<br /><br /> 默认值为 65507。|  
|maxUnicastRetransmitCount|一个整数，指定应重新传输消息的最大次数（包括第一次发送）。  如果将消息发送到单播地址，并且收到的响应消息中带有相应的 RelatesTo 标头，重新传输可能会提前终止（在达到配置的重新传输次数之前）。<br /><br /> 默认值为 1。|  
|multicastInterfaceId|一个字符串，唯一标识在多宿主计算机上发送和接收多播流量时应使用的网络适配器。  在运行时，传输将使用此特性值来查找接口索引，然后使用该索引设置 `IP_MULTICAST_IF` 和 `IPV6_MULTICAST_IF` 套接字选项。  加入多播组时将使用相同的接口索引（如果适用）。<br /><br /> 默认值为 `null`。|  
|socketReceiveBufferSize|一个整数，指定基础 WinSock 套接字上接收缓冲区的大小。<br /><br /> 接收通道的用户可以对绑定使用此特性，以控制系统在接收数据时的行为。  例如，假定应用程序使用入站 WCF 消息时达到了最大阈值，对此特性使用较高的值将允许消息在等待应用程序处理时在 WinSock 缓冲区中堆叠。  在相同情况下使用较低的值将导致丢弃这些消息。此特性公开基础 WinSock `SO_RCVBUF` 套接字选项。此特性值必须至少为 `maxReceivedMessageSize` 的大小。  如果将此特性值设置为小于 `maxReceivedMessageSize` 的值，会导致运行时异常。<br /><br /> 默认值为 65536。|  
|timeToLive|一个整数，指定多播数据包可以遍历的网络段跃点数。  此特性公开与 `IP_MULTICAST_TTL` 和 `IP_TTL` 套接字选项关联的功能。<br /><br /> 默认值为 1。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<udpDiscoveryEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/udpdiscoveryendpoint.md)|具有固定发现协定和 UDP 传输绑定的标准终结点。|  
  
## 请参阅  
 <xref:System.Servicemodel.Discovery.UdpTransportSettings>