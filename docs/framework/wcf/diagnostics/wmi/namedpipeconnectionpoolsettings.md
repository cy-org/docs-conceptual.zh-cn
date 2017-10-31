---
title: "NamedPipeConnectionPoolSettings | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 079bccb8-54b5-4436-a43d-5567763f72ce
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# NamedPipeConnectionPoolSettings
NamedPipeConnectionPoolSettings  
  
## 语法  
  
```  
class NamedPipeConnectionPoolSettings  
{  
  string GroupName;  
  datetime IdleTimeout;  
  sint32 MaxOutboundConnectionsPerEndpoint;  
};  
```  
  
## 方法  
 NamedPipeConnectionPoolSettings 类不定义任何方法。  
  
## 属性  
 NamedPipeConnectionPoolSettings 类具有以下属性：  
  
### GroupName  
 数据类型：String  
  
 访问类型：只读  
  
 绑定元素使用的连接池的组名。  
  
### IdleTimeout  
 数据类型：DateTime  
  
 访问类型：只读  
  
 连接在断开前可以空闲的最长时间。  
  
### MaxOutboundConnectionsPerEndpoint  
 数据类型：sint32  
  
 访问类型：只读  
  
 客户端上每个终结点的最大出站连接数。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.NamedPipeConnectionPoolSettings>