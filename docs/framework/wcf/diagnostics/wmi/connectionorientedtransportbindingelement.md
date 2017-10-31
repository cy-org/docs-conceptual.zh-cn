---
title: "ConnectionOrientedTransportBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1308313-f0e2-49e6-977d-6b4ce9ad35d1
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ConnectionOrientedTransportBindingElement
ConnectionOrientedTransportBindingElement  
  
## 语法  
  
```  
class ConnectionOrientedTransportBindingElement : TransportBindingElement  
{  
  datetime ChannelInitializationTimeout;  
  sint32 ConnectionBufferSize;  
  string HostNameComparisonMode;  
  sint32 MaxBufferSize;  
  datetime MaxOutputDelay;  
  sint32 MaxPendingAccepts;  
  sint32 MaxPendingConnections;  
  string TransferMode;  
};  
```  
  
## 方法  
 ConnectionOrientedTransportBindingElement 类不定义任何方法。  
  
## 属性  
 ConnectionOrientedTransportBindingElement 类具有以下属性：  
  
### ChannelInitializationTimeout  
 数据类型：DateTime  
  
 访问类型：只读  
  
 指定在超时前可用于完成通道初始化的时间间隔。  
  
### ConnectionBufferSize  
 数据类型：sint32  
  
 访问类型：只读  
  
 用于从客户端或服务传输网络上的序列化消息块的缓冲区大小。  
  
### HostNameComparisonMode  
 数据类型：String  
  
 访问类型：只读  
  
 一个值，指示在对 URI 进行匹配时，是否使用主机名来访问服务。  
  
### MaxBufferSize  
 数据类型：sint32  
  
 访问类型：只读  
  
 要使用的缓冲区最大大小。  
  
### MaxOutputDelay  
 数据类型：DateTime  
  
 访问类型：只读  
  
 消息块或完整消息在发出之前可以在内存中保持缓冲的最大时间间隔。  
  
### MaxPendingAccepts  
 数据类型：sint32  
  
 访问类型：只读  
  
 可用于处理服务上的传入连接的最大挂起异步接受线程数。  
  
### MaxPendingConnections  
 数据类型：sint32  
  
 访问类型：只读  
  
 最大挂起连接数。  
  
### TransferMode  
 数据类型：String  
  
 访问类型：只读  
  
 一个值，指定通过面向连接的传输对消息进行缓冲还是流处理。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>