---
title: "ReliableSessionBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: effda125-b8d3-4de6-8c0e-f59f5ea8f6eb
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# ReliableSessionBindingElement
ReliableSessionBindingElement  
  
## 语法  
  
```  
class ReliableSessionBindingElement : BindingElement  
{  
  datetime AcknowledgementInterval;  
  boolean FlowControlEnabled;  
  datetime InactivityTimeout;  
  sint32 MaxPendingChannels;  
  sint32 MaxRetryCount;  
  sint32 MaxTransferWindowSize;  
  boolean Ordered;  
  integer ReliableMessagingVersion;  
};  
```  
  
## 方法  
 ReliableSessionBindingElement 类未定义任何方法。  
  
## 属性  
 ReliableSessionBindingElement 类具有下列属性：  
  
### AcknowledgementInterval  
 数据类型：DateTime  
  
 访问类型：只读  
  
 向工厂创建的可靠通道上的消息源发送确认之前目标等待的时间间隔。  
  
### FlowControlEnabled  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个布尔值，指定是否启用流控制。  
  
### InactivityTimeout  
 数据类型：DateTime  
  
 访问类型：只读  
  
 指定通道出错之前，通道允许其他通信方不发送任何消息的最长持续时间。  
  
### MaxPendingChannels  
 数据类型：sint32  
  
 访问类型：只读  
  
 侦听器上可等待接受的最大通道数。  
  
### MaxRetryCount  
 数据类型：sint32  
  
 访问类型：只读  
  
 可靠通道未收到消息确认时，通过在其基础通道上调用 `Send` 尝试重新传输该消息的最多尝试次数。  
  
### MaxTransferWindowSize  
 数据类型：sint32  
  
 访问类型：只读  
  
 可靠会话的最大传输窗口大小。  
  
### Ordered  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个布尔值，指定是否保证消息以其发送顺序抵达。  
  
### ReliableMessagingVersion  
 数据类型：Integer  
  
 访问类型：只读  
  
 一个整数，指定可靠会话中使用的 WS\-ReliableMessaging 协议版本。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>