---
title: "&lt;namedCaches&gt; 元素（缓存设置） | Microsoft Docs"
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
  - "<namedCaches> 元素"
  - "缓存 [.NET Framework], 配置"
  - "namedCaches 元素"
ms.assetid: 6bd4fbc5-55a6-4dc4-998b-cdcc7e023330
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# &lt;namedCaches&gt; 元素（缓存设置）
指定命名的 <xref:System.Runtime.Caching.MemoryCache> 实例的配置设置的集合。  <xref:System.Runtime.Caching.Configuration.MemoryCacheSection.NamedCaches%2A> 属性从配置文件的一个或多个 `namedCaches` 元素中引用配置设置的集合。  
  
## 语法  
  
```  
<namedCaches>  
  <add name="default"   
</namedCaches>  
```  
  
## 类型  
 `None`  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`CacheMemoryLimitMegabytes`|指定 <xref:System.Runtime.Caching.MemoryCache> 的实例可增长到的最大允许大小（以兆字节为单位）的整数值。  默认值是 0，表示默认使用 <xref:System.Runtime.Caching.MemoryCache> 类的自动调整大小试探法。|  
|`Name`|缓存的名称。|  
|`PhysicalMemoryLimitPercentage`|介于 0 与 100 之间的指定高速缓存可以使用的物理安装的计算机内存的最大百分比的整数值。  默认值是 0，表示默认使用 <xref:System.Runtime.Caching.MemoryCache> 类的自动调整大小试探法。|  
|`PollingInterval`|一个值，该值指示缓存实现将当前内存负载与为缓存实例设置的绝对内存和内存百分比限制进行比较所采用的时间间隔。  此值以“HH:MM:SS”格式输入。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/runtime/add-element-for-namedcaches.md)|向内存缓存的 `namedCaches` 集合添加已命名的高速缓存。|  
|[\<clear\>](../../../../../docs/framework/configure-apps/file-schema/runtime/clear-element-for-namedcaches.md)|清除内存缓存的 `namedCaches` 集合。|  
|[\<remove\>](../../../../../docs/framework/configure-apps/file-schema/runtime/remove-element-for-namedcaches.md)|从内存缓存的 `namedCaches` 集合移除已命名的高速缓存。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<memoryCache\>](../../../../../docs/framework/configure-apps/file-schema/runtime/memorycache-element-cache-settings.md)|定义一个元素，该元素用于配置基于 <xref:System.Runtime.Caching.MemoryCache> 类的缓存。|  
  
## 备注  
 Web.config 文件的内存缓存配置节可以包含 `namedCaches` 集合的 `add`、`remove` 和 `clear` 特性。  每个 `namedCaches` 项均通过 `name` 特性唯一标识。  
  
 您可以通过引用应用程序配置文件中的信息来检索内存缓存项的实例。  默认情况下，只有默认的高速缓存实例包含在配置文件中。  默认缓存实例是从 <xref:System.Runtime.Caching.MemoryCache.Default%2A> 属性返回的实例。  
  
 如果将名称特性设置为“默认”，则元素将使用默认的内存缓存实例。  
  
## 示例  
 下面的示例演示如何通过将 `name` 特性设置为“默认”将缓存的名称设置为默认缓存项名称。  
  
 `cacheMemoryLimitMegabytes` 特性和 `physicalMemoryPercentage` 特性被设置为零。  将这些特性设置为零意味着使用 <xref:System.Runtime.Caching.MemoryCache> 类的自动调整大小试探法。  每隔两分钟，缓存实现将当前内存负载与基于百分比的绝对内存限制进行比较。  
  
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
 [\<memoryCache\> 元素（缓存设置）](../../../../../docs/framework/configure-apps/file-schema/runtime/memorycache-element-cache-settings.md)