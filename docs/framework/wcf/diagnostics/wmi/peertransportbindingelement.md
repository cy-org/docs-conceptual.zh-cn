---
title: "PeerTransportBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 40bf6be2-8087-4cb3-a66c-408d53eb9269
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# PeerTransportBindingElement
PeerTransportBindingElement  
  
## 语法  
  
```  
class PeerTransportBindingElement : TransportBindingElement  
{  
  string ListenIPAddress;  
  sint32 Port;  
  PeerSecuritySettings Security;  
};  
```  
  
## 方法  
 PeerTransportBindingElement 类未定义任何方法。  
  
## 属性  
 PeerTransportBindingElement 类具有以下属性：  
  
### ListenIPAddress  
 数据类型：String  
  
 访问类型：只读  
  
 对等节点在其上侦听消息的 IP 地址。  
  
### Port  
 数据类型：sint32  
  
 访问类型：只读  
  
 网络接口端口，此绑定在该端口上处理对等通道消息。  
  
### Security  
 数据类型：PeerSecuritySettings  
  
 访问类型：只读  
  
 对等传输安全设置。  
  
## 要求  
  
|MOF|在 Servicemodel.mof 中声明。|  
|---------|-----------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.PeerTransportBindingElement>