---
title: "TcpTransportBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 33bbc1e5-44e4-4ee3-b7b5-801dc78956e4
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# TcpTransportBindingElement
TcpTransportBindingElement  
  
## 语法  
  
```  
class TcpTransportBindingElement : ConnectionOrientedTransportBindingElement  
{  
  TcpConnectionPoolSettings ConnectionPoolSettings;  
  sint32 ListenBacklog;  
  boolean PortSharingEnabled;  
  boolean TeredoEnabled;  
};  
```  
  
## 方法  
 TcpTransportBindingElement 类不定义任何方法。  
  
## 属性  
 TcpTransportBindingElement 类具有以下属性：  
  
### ConnectionPoolSettings  
 数据类型：TcpConnectionPoolSettings  
  
 访问类型：只读  
  
 连接池设置。  
  
### ListenBacklog  
 数据类型：sint32  
  
 访问类型：只读  
  
 可挂起的最大排队连接请求数。  
  
### PortSharingEnabled  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个布尔值，指定是否为此连接启用 TCP 端口共享。  
  
### TeredoEnabled  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个布尔值，指定是否启用 Teredo（一种用于对防火墙后的客户端进行寻址的技术）。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.TcpTransportBindingElement>