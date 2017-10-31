---
title: "发现版本控制 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f91c6d0a-3af2-45c5-9a5c-e75390619836
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 发现版本控制
本主题简要概述了一些新增发现功能的实现，  还概述了如何选择要使用的发现版本。  
  
## 发现版本控制  
 发现功能包括对 WS\_Discovery 协议的三个版本的支持。  使用发现 API，您可以选择要使用的协议版本。  本文档简要介绍与版本控制相关的设置。  
  
 下面的发现类现在具有 <xref:System.ServiceModel.Discovery.DiscoveryVersion> 属性，并在其构造函数中采用 <xref:System.ServiceModel.Discovery.DiscoveryVersion> 参数：  
  
-   <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>  
  
### DiscoveryVersion.WSDiscoveryApril2005  
 作为构造函数参数提供 <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryApril2005> 可使实现使用 WS\-Discovery 协议的 April2005 版本。  此版本对应于 WS\-Discovery 协议规范的已发布版本。  此版本应当用于与使用 April2005 版 WS\-Discovery 的旧版应用程序进行互操作。  
  
### DiscoveryVersion.WSDiscovery11  
 API 使用的默认发现版本是 <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscovery11>。  这是 WS\-Discovery 协议的当前标准化版本。  
  
## DiscoveryVersion.WSDiscoveryCD1  
 作为构造函数参数提供 <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryCD1> 可使实现使用 WS\-Discovery 协议的委员会草案第 1 版。  此协议版本应当用于与运行 CD1 版 WS\-Discovery 协议的实现进行互操作。  
  
## 支持单一服务主机上不同发现版本的多个 UDP 发现终结点  
 您可能希望在单一服务主机上对不同发现版本公开多个 UDP 发现终结点。  为此，必须为每个 UDP 发现终结点指定唯一的地址。  下面的示例演示如何执行此操作。  
  
```  
UdpDiscoveryEndpoint newVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscovery11);  
UdpDiscoveryEndpoint oldVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);  
  
newVersionUdpEndpoint.Address = new EndpointAddress(newVersionUdpEndpoint.Address.Uri.ToString() + "/version11");  
oldVersionUdpEndpoint.Address = new EndpointAddress(oldVersionUdpEndpoint.Address.Uri.ToString() + "/versionAril2005");  
  
serviceHost.AddServiceEndpoint(newVersionUdpEndpoint);  
serviceHost.AddServiceEndpoint(oldVersionUdpEndpoint);  
  
```