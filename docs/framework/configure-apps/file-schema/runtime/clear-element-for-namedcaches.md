---
title: "&lt;namedCaches&gt; 的 &lt;clear&gt; 元素 | Microsoft Docs"
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
  - "<namedCaches> 的 <clear> 元素"
  - "<namedCaches> 的 clear 元素"
ms.assetid: ea01a858-65da-4348-800f-5e3df59d4d79
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# &lt;namedCaches&gt; 的 &lt;clear&gt; 元素
清除内存缓存的 `namedCaches` 集合中的所有 `namedCache` 项。  
  
## 语法  
  
```  
<namedCaches>  
    <clear name="default" />  
    <!-- child elements -->  
 </namedCaches>  
```  
  
## 类型  
 `Type`  
  
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
 `clear` 元素清除内存缓存的命名的缓存集合中的所有 `namedCache` 项。  在使用 `add` 元素添加新命名的高速缓存项之前，可以使用 `clear` 元素来保证该集合中没有其他已命名的高速缓存。  
  
## 请参阅  
 [\<namedCaches\> 元素（缓存设置）](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)