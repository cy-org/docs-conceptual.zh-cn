---
title: "Service | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 999806e1-6376-409e-b998-b0af391adfe7
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Service
服务  
  
## 语法  
  
```  
class Service  
{  
  string BaseAddresses[];  
  Behavior Behaviors[];  
  string ConfigurationName;  
  string CounterInstanceName;  
  string DistinguishedName;  
  string Extensions[];  
  string Metadata[];  
  string Name;  
  string Namespace;  
  datetime Opened;  
  Channel OutgoingChannels[];  
  sint32 ProcessId;  
};  
```  
  
## 方法  
 Service 类未定义任何方法。  
  
## 属性  
 Service 类具有以下属性：  
  
### BaseAddresses  
 数据类型：String array  
  
 访问类型：只读  
  
 服务使用的基址。  
  
### Behaviors  
 数据类型：Behavior array  
  
 访问类型：只读  
  
 与此服务关联的行为。  
  
### ConfigurationName  
 数据类型：String  
  
 访问类型：只读  
  
 ServiceElement\_BehaviorConfiguration  
  
### CounterInstanceName  
 数据类型：String  
  
 访问类型：只读  
  
 此服务的性能计数器实例的实例名称。  
  
### DistinguishedName  
 数据类型：String  
  
 访问类型：只读  
  
 该地址处的服务名称。  
  
### Extensions  
 数据类型：String array  
  
 访问类型：只读  
  
 服务实例扩展的实例上下文。  
  
### Metadata  
 数据类型：String array  
  
 访问类型：只读  
  
 服务元数据设置。  
  
### Name  
 数据类型：String  
  
 访问类型：只读  
  
 此服务的唯一名称。  
  
### Namespace  
 数据类型：String  
  
 访问类型：只读  
  
 服务的命名空间。  
  
### Opened  
 数据类型：DateTime  
  
 访问类型：只读  
  
 服务打开的时间。  
  
### OutgoingChannels  
 数据类型：Channel array  
  
 访问类型：只读  
  
 从服务实例传出的通道。  
  
### ProcessId  
 数据类型：sint32  
  
 访问类型：只读  
  
 承载服务的进程的进程 ID。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|