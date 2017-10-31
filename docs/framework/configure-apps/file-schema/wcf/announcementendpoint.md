---
title: "&lt;announcementEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 034b7c69-a770-4502-8cef-38007bbcd025
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;announcementEndpoint&gt;
此配置元素定义具有固定公告协定的标准终结点。  当分别打开或关闭服务时，服务可以选择通过发送一条联机和脱机公告消息来公告其可用性。  [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 服务在 [\<serviceDiscovery\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicediscovery.md) 元素中指定公告终结点，并使用 AnnouncementClient 执行公告。  如果客户端希望侦听来自其他服务的公告，它实际充当的是 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务；因此，必须在 [\<服务\>](../../../../../docs/framework/configure-apps/file-schema/wcf/services.md) 节中为该客户端配置公告终结点。  
  
## 语法  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <announcementEndpoint>   
          <standardEndpoint  
                  discoveryVersion=”WSDiscovery11/WSDiscoveryApril2005”  
                  maxAnnouncementDelay=”Timespan”   
                  name="String" />   
       </announcementEndpoint>          
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|discoveryVersion|一个字符串，指定两个 WS\-Discovery 协议版本中的其中一个版本。  有效值为 WSDiscovery11 和 WSDiscoveryApril2005。  此值的类型为 <xref:System.ServiceModel.Discovery.Configuration.DiscoveryVersion>。|  
|maxAnnouncementDelay|一个 Timespan 值，指定 Discovery 协议在发送 Hello 消息之前等待的最大延迟值。  消息在发送之前将等待一个随机时间值（介于 0 到此特性值之间）。  此特性用于设置随机的短时间延迟，以防止在网络出现故障后所有服务同时重新联机所造成的网络风暴。|  
|name|一个字符串，指定标准终结点的配置的名称。  此名称在服务终结点的 `endpointConfiguration` 特性中用于将标准终结点链接到其配置。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|具有一个或多个固定属性（地址、绑定和协定）的预定义终结点的标准终结点集合。|  
  
## 示例  
 下面的示例演示通过 http 和对等网络侦听公告消息的客户端。  
  
```  
  
<services>  
  <service name="ServiceAnnouncementListener">  
              <endpoint name="httpAnnouncementEndpoint"  
                        kind="announcementEndpoint"  
                        binding="basicHttpBinding"  
                        address="announcements" />  
              <endpoint name="peerNetAnnouncementEndpoint"  
                        kind="announcementEndpoint"  
                        binding="peerTcpBinding"  
                        address="net.p2p://discoveryMesh/multicast"  
                        bindingConfiguration="discoveryPeerTcpBindingConfig" />  
  ...  
  </service>  
</services>  
  
<standardEndpoints>  
  <announcementEndpoint>  
     <standardEndpoint name="httpAnnouncementEndpoint"                         
                       version="WSDiscoveryApril2005" />  
     <standardEndpoint name="peerNetAnnouncementEndpoint"                         
                       version="WSDiscoveryApril2005" />  
   </announcementEndpoint>  
</standardEndpoints>  
  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>