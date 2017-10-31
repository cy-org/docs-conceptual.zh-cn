---
title: "MsmqBindingElementBase | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 210d41ab-a2a4-4d7a-afd2-0916c08a4015
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# MsmqBindingElementBase
MsmqBindingElementBase  
  
## 语法  
  
```  
class MsmqBindingElementBase : TransportBindingElement  
{  
  string CustomDeadLetterQueue;  
  string DeadLetterQueue;  
  boolean Durable;  
  boolean ExactlyOnce;  
  sint32 MaxRetryCycles;  
  string ReceiveErrorHandling;  
  sint32 ReceiveRetryCount;  
  datetime RetryCycleDelay;  
  datetime TimeToLive;  
  boolean UseMsmqTracing;  
  boolean UseSourceJournal;  
};  
```  
  
## 方法  
 MsmqBindingElementBase 类不定义任何方法。  
  
## 属性  
 MsmqBindingElementBase 类具有以下属性：  
  
### CustomDeadLetterQueue  
 数据类型：String  
  
 访问类型：只读  
  
 一个 URI，其中包含每个应用程序的死信队列位置（用于放置已过期的消息或传输\/传递失败的消息的位置）。  
  
### DeadLetterQueue  
 数据类型：String  
  
 访问类型：只读  
  
 一个枚举值，指示要使用的死信队列的类型。  
  
### Durable  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个值，指示此绑定处理的消息是持久的还是可变的。  
  
### ExactlyOnce  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个 Boolean 值，指示是否只接收过一次此绑定处理的消息。  
  
### MaxRetryCycles  
 数据类型：sint32  
  
 访问类型：只读  
  
 尝试向接收应用程序传递消息的最大重试周期数。  
  
### ReceiveErrorHandling  
 数据类型：String  
  
 访问类型：只读  
  
 病毒消息处理设置。  
  
### ReceiveRetryCount  
 数据类型：sint32  
  
 访问类型：只读  
  
 从应用程序队列读取消息的最大立即重试次数。  
  
### RetryCycleDelay  
 数据类型：DateTime  
  
 访问类型：只读  
  
 一个值，指示尝试传递无法立即传递的消息时，重试周期之间的时间延迟。  
  
### TimeToLive  
 数据类型：DateTime  
  
 访问类型：只读  
  
 时间间隔，指示此绑定所处理的消息在过期之前可以保留在队列中的时间。  
  
### UseMsmqTracing  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个 Boolean 值，指示是否应跟踪此绑定处理的消息。  
  
### UseSourceJournal  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个 Boolean 值，指示此绑定所处理的消息副本是否应存储在源日志队列中。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.NetMsmqBinding>   
 <xref:System.ServiceModel.MsmqBindingBase>