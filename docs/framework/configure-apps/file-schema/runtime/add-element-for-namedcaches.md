---
title: "&lt;namedCaches&gt; 的 &lt;add&gt; 元素 | Microsoft Docs"
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
  - "<namedCaches> 的 <add> 元素"
  - "<namedCaches> 的 add 元素"
ms.assetid: ce2a63a8-c829-4742-a6ea-72ee5d89f169
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# &lt;namedCaches&gt; 的 &lt;add&gt; 元素
向内存缓存的 `namedCaches` 集合添加 `namedCache` 项。  
  
## 语法  
  
```  
<namedCaches>  
    <add name="default" />  
      <!-- child elements -->  
 </namedCaches>  
```  
  
## 类型  
 `None`  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|||  
|-|-|  
|特性|说明|  
|`CacheMemoryLimitMegabytes`|指定 <xref:System.Runtime.Caching.MemoryCache> 的实例可增长到的最大允许大小（以兆字节为单位）的整数值。  默认值是 0，表示默认使用 <xref:System.Runtime.Caching.MemoryCache> 类的自动调整大小试探法。|  
|`Name`|缓存的名称。|  
|`PhysicalMemoryLimitPercentage`|介于 0 与 100 之间的指定高速缓存可以使用的物理安装的计算机内存的最大百分比的整数值。  默认值是 0，表示默认使用 <xref:System.Runtime.Caching.MemoryCache> 类的自动调整大小试探法。|  
|`PollingInterval`|一个值，该值指示缓存实现将当前内存负载与为缓存实例设置的绝对内存和内存百分比限制进行比较所采用的时间间隔。  此值以“HH:MM:SS”格式输入。|  
  
### 子元素  
 `None`  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<namedCaches\>](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)|包含命名的 <xref:System.Runtime.Caching.MemoryCache> 实例的配置设置的集合。|  
  
## 备注  
 `add` 元素向用于内存缓存的 `namedCaches` 集合添加项  在使用 `add` 元素之前，可以使用 [clear](../../../../../docs/framework/configure-apps/file-schema/runtime/clear-element-for-namedcaches.md) 元素来保证该集合中没有其他已命名的高速缓存。  此元素可用于 Machine.config 文件和 Web.config 文件中。  
  
## 示例  
 下面的示例演示如何定义默认 `namedCache` 项对内存缓存的 `namedCaches`  集合的设置。  
  
```  
<configuration>  
  
  <system.runtime.caching>  
    <memoryCache>  
      <namedCaches>  
          <add name="default"   
               cacheMemoryLimitMegabytes="0"   
               physicalMemoryPercentage="0"  
               pollingInterval="00:02:00" />  
      </namedCaches>  
    </memoryCache>  
  </system.runtime.caching>  
  
</configuration>  
```  
  
## 请参阅  
 [\<namedCaches\> 元素（缓存设置）](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)