---
title: "Channel 类 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d9fae2ca-209c-4341-a0f5-6b79d1a67776
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Channel 类
通道  
  
## 语法  
  
```  
class Channel  
{  
  string LocalAddress;  
  Endpoint ref;  
  string RemoteAddress;  
  string SessionId;  
  string Type;  
};  
```  
  
## 方法  
 Channel 类未定义任何方法。  
  
## 属性  
 Channel 类具有以下属性。  
  
### LocalAddress  
 数据类型：String  
  
 访问类型：只读  
  
 通道的本地终结点。  
  
### ref  
 数据类型：Endpoint  
  
 访问类型：只读  
  
 对通道所连接到的终结点的引用。  
  
### RemoteAddress  
 数据类型：String  
  
 访问类型：只读  
  
 与通道相关联的远程地址。  
  
### SessionId  
 数据类型：String  
  
 访问类型：只读  
  
 当前会话的 ID（如果有）。  
  
### 类型  
 数据类型：String  
  
 访问类型：只读  
  
 通道的类型。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.ChannelBase>