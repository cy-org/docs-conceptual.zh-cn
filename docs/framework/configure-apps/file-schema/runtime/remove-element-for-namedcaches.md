---
title: "&lt;namedCaches&gt; 的 &lt;remove&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "namedCaches 的 <remove> 元素"
  - "namedCaches 的 remove 元素"
ms.assetid: 24211ea5-163e-4fe5-aed8-004d8499760c
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# &lt;namedCaches&gt; 的 &lt;remove&gt; 元素
从内存缓存的 `namedCaches` 集合移除已命名的高速缓存。  
  
## 语法  
  
```  
<namedCaches>  
    <remove name="default" />  
    <!-- child elements -->  
 </namedCaches>  
```  
  
## 类型  
 `None`  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
 `None`  
  
### 子元素  
 `None`  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<namedCaches\>](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)|包含命名的 <xref:System.Runtime.Caching.MemoryCache> 实例的配置设置的集合。|  
  
## 备注  
 `remove` 元素从内存缓存的命名缓存集合中移除 `namedCache` 项。  
  
## 请参阅  
 [\<namedCaches\> 元素（缓存设置）](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)