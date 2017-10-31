---
title: "MsmqTransportBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c89f073-9ed3-4025-a8c5-13535a0f526b
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# MsmqTransportBindingElement
MsmqTransportBindingElement  
  
## 语法  
  
```  
class MsmqTransportBindingElement : MsmqBindingElementBase  
{  
  sint32 MaxPoolSize;  
  string QueueTransferProtocol;  
  boolean UseActiveDirectory;  
};  
```  
  
## 方法  
 MsmqTransportBindingElement 类不定义任何方法。  
  
## 属性  
 MsmqTransportBindingElement 类具有以下属性：  
  
### MaxPoolSize  
 数据类型：sint32  
  
 访问类型：只读  
  
 包含内部 MSMQ 消息对象的池的最大大小。  
  
### QueueTransferProtocol  
 数据类型：String  
  
 访问类型：只读  
  
 一个枚举值，指示此绑定使用的排队通信通道传输。  
  
### UseActiveDirectory  
 数据类型：Boolean  
  
 访问类型：只读  
  
 返回一个 Boolean 值，该值指示是否应该使用 Active Directory 转换队列地址。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>