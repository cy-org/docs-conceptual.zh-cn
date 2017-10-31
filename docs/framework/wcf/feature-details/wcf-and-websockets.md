---
title: "WCF 和 WebSocket | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1e53b49e-022c-49c7-8984-4b21b53c05b3
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# WCF 和 WebSocket
.NET Framework 4.5 引入了对 Windows Communication Foundation 中的 WebSocket 的支持。WebSocket 是一种高效的、基于标准的技术，可通过标准 HTTP 端口 80 和 443 实现双向通信。使用标准 HTTP 端口，WebSocket 可通过中介跨 Web 进行通信。添加了两个新的标准绑定以支持通过 WebSocket 传输进行的通信。<xref:System.ServiceModel.NetHttpBinding> 和 <xref:System.ServiceModel.NetHttpsBinding>。通过访问 <xref:System.ServiceModel.Channels.HttpTransportBindingElement.WebSocketSettings%2A> 属性，可在 <xref:> System.ServiceModel.Channels.HttpTransportBinding?qualifyHint=False&autoUpgrade=True 元素上对 WebSocket 特定设置进行配置。  
  
## 本节内容  
 [使用 NetHttpBinding](../../../../docs/framework/wcf/feature-details/using-the-nethttpbinding.md)  
 讨论 <xref:System.ServiceModel.NetHttpBinding> 以及如何对其进行配置。  
  
 [如何创建通过 WebSocket 进行通信的 WCF 服务](../../../../docs/framework/wcf/feature-details/how-to-create-a-wcf-service-that-communicates-over-websockets.md)  
 说明如何创建通过 Websocket 进行通信的 WCF 服务。  
  
## 参考  
  
## 相关章节