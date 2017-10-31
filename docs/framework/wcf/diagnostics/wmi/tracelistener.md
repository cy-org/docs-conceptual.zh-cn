---
title: "TraceListener | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c2c0b595-a384-4eb3-b94d-1b3be7cc7a5c
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# TraceListener
TraceListener。  
  
## 语法  
  
```  
class TraceListener  
{  
  string Name;  
  TraceListenerArgument TraceListenerArguments[];  
};  
```  
  
## 方法  
 TraceListener 类不定义任何方法。  
  
## 属性  
 TraceListener 类具有以下属性：  
  
### 名称  
 数据类型：String  
  
 访问类型：只读  
  
 跟踪侦听器的名称。  
  
### TraceListenerArguments  
 数据类型：TraceListenerArgument 数组  
  
 访问类型：只读  
  
 跟踪侦听器的参数。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|