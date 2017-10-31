---
title: "ServiceToEndpointAssociation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 03c3cd15-e1b2-4dc2-bdc2-59fdccdae110
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ServiceToEndpointAssociation
将服务映射到终结点。  
  
## 语法  
  
```  
class ServiceToEndpointAssociation  
{  
  Service ref;  
  Endpoint ref;  
};  
```  
  
## 方法  
 ServiceToEndpointAssociation 类不定义任何方法。  
  
## 属性  
 ServiceToEndpointAssociation 类有以下属性：  
  
### ref  
 数据类型：Service  
  
 访问类型：只读  
限定符：键  
  
 与终结点关联的服务。  
  
### ref  
 数据类型：Endpoint  
  
 访问类型：只读  
限定符：键  
  
 与服务关联的终结点。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|