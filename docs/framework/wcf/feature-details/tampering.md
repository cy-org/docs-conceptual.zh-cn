---
title: "篡改 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3bad93be-60bb-4f89-96ab-a1c3dc7c0fad
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 篡改
*篡改*是一种更改消息或消息的传递方式，并将更改后的消息用于非原有用途的其他用途的行为。  
  
## 不要禁用 WS\-Addressing  
 WS\-Addressing 规范在每条消息中提供了地址标头，从而允许消息接收方验证消息的发送方。将 <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> 属性设置为 <xref:System.ServiceModel.Channels.AddressingVersion.None%2A> 可禁用此功能。  
  
 当安全模式设置为“消息”并且禁用了 WS\-Addressing 时，攻击者就能获取来自客户端的请求，并将其发送到另一个服务，而第二个服务无法检测该消息是否来自于原客户端。实际上，第一个服务在与第二个服务通信时，可假装它是一个客户端。  
  
 为了避免这个问题，请不要将 <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> 属性设置为 <xref:System.ServiceModel.Channels.AddressingVersion.None%2A>，并避免使用 <xref:System.ServiceModel.Channels.MessageVersion>，如静态 <xref:System.ServiceModel.Channels.MessageVersion.Soap12%2A> 属性，它会将 <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> 属性设置为 <xref:System.ServiceModel.Channels.AddressingVersion.None%2A>。  
  
## 请参阅  
 [安全注意事项](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)   
 [信息泄露](../../../../docs/framework/wcf/feature-details/information-disclosure.md)   
 [特权提升](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)   
 [拒绝服务](../../../../docs/framework/wcf/feature-details/denial-of-service.md)   
 [不支持的方案](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)   
 [重播攻击](../../../../docs/framework/wcf/feature-details/replay-attacks.md)