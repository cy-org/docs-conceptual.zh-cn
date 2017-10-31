---
title: "&lt;discoveryEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fae2f48b-a635-4e4b-859d-a1432ac37e1c
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;discoveryEndpoint&gt;
此配置元素定义具有固定发现协定的标准终结点。  将此元素添加到服务配置后，该元素将指定侦听发现消息的位置。  将此元素添加到客户端配置后，该元素将指定发送发现查询的位置。  
  
## 语法  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <discoveryEndpoint>   
          <standardEndpoint  
                  discoveryMode=”Adhoc/Managed”  
                  discoveryVersion=”WSDiscovery11/WSDiscoveryApril2005”  
                  maxResponseDelay=”Timespan”   
                  name="String" />  
       </discoveryEndpoint>          
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|discoveryMode|一个字符串，指定发现协议的模式。  有效值为“Adhoc”和“Managed”。  在托管模式下，协议依靠发现代理，此代理用作可检测服务的存储库。  即席模式要求协议使用 UDP 多播机制查找可用的服务。  此值的类型为 <xref:System.Servicemodel.Discovery.DiscoveryMode>。|  
|discoveryVersion|一个字符串，指定两个 WS\-Discovery 协议版本中的其中一个版本。  有效值为 WSDiscovery11 和 WSDiscoveryApril2005。  此值的类型为 <xref:System.Servicemodel.Discovery.DiscoveryVersion>。|  
|maxResponseDelay|一个 Timespan 值，指定 Discovery 协议在发送 Probe Match、Resolve Match 这类消息之前等待的最大延迟值。<br /><br /> 如果同时发送所有 ProbeMatch，则可能发生网络风暴。  若要防止发生这种情况，可在发送 ProbeMatch 时在各 ProbeMatch 之间应用随机延迟。  随机延迟的范围是从 0 到此特性所设置的值之间。  如果将此特性设置为 0，则在不使用任何延迟的紧凑循环中发送 ProbeMatch 消息。  否则，在发送 ProbeMatch 消息时将应用一定的随机延迟，以使发送所有 ProbeMatch 消息所用的总时间不会超过 maxResponseDelay。  此值只与服务相关，不可用于客户端。|  
|`name`|一个字符串，指定标准终结点的配置的名称。  此名称在服务终结点的 `endpointConfiguration` 特性中用于将标准终结点链接到其配置。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|具有一个或多个固定属性（地址、绑定和协定）的预定义终结点的标准终结点集合。|  
  
## 示例  
 下面的示例演示通过对等网多播传输侦听发现消息的服务。  此示例明确指定 WS\-Discovery 2005 年 4 月版。  
  
 标准终结点配置基于服务定义，无法在服务之间共享。  如果其他服务希望采用相同的发现终结点，则需要将相同配置添加到该服务的节中。  
  
```  
  
<services>  
    <service name="CalculatorService"  
             behaviorConfiguration="CalculatorServiceBehavior">  
             <endpoint binding="basicHttpBinding"   
                address="calculator" contract="ICalculatorService" />  
             <endpoint name="peerNetDiscovery"  
                binding="peerTcpBinding"  
                address="net.p2p://discoveryMesh/multicast"  
                kind="discoveryEndpoint"  
                endpointConfiguration="peerTcpDiscoveryEndpointConfiguration"  
                bindingConfiguration="discoveryPeerTcpBindingConfig" />      
   </service>  
</services>  
<standardEndpoints>  
  <discoveryEndpoint>  
     <standardEndpoint name="peerTcpDiscoveryEndpointConfiguration "                         
                       version="WSDiscoveryApril2005" />  
   </discoveryEndpoint>  
</standardEndpoints>  
  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>