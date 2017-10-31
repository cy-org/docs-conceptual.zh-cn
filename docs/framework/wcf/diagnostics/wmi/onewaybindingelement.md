---
title: "OneWayBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5c7e17c3-39b9-4214-ae08-9e6141734305
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# OneWayBindingElement
OneWayBindingElement  
  
## 语法  
  
```  
class OneWayBindingElement : BindingElement  
{  
  ChannelPoolSettings ChannelPoolSettings;  
  sint32 MaxAcceptedChannels;  
  boolean PacketRoutable;  
};  
```  
  
## 方法  
 OneWayBindingElement 类未定义任何方法。  
  
## 属性  
 OneWayBindingElement 类具有以下属性：  
  
### ChannelPoolSettings  
 数据类型：ChannelPoolSettings  
  
 访问类型：只读  
  
 通道池设置。  
  
### MaxAcceptedChannels  
 数据类型：sint32  
  
 访问类型：只读  
  
 接受的最大通道数。  
  
### PacketRoutable  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个值，该值指示数据包是否可路由。  
  
## 要求  
  
|MOF|在 Servicemodel.mof 中声明。|  
|---------|-----------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.OneWayBindingElement>