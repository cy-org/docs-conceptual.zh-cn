---
title: "&lt;memoryCache&gt; 元素（缓存设置） | Microsoft Docs"
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
  - "<memoryCache> 元素"
  - "缓存 [.NET Framework], 配置"
  - "memoryCache 元素"
ms.assetid: 182a622f-f7cf-472d-9d0b-451d2fd94525
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# &lt;memoryCache&gt; 元素（缓存设置）
定义一个用于配置基于 <xref:System.Runtime.Caching.MemoryCache> 类的缓存的元素。<xref:System.Runtime.Caching.Configuration.MemoryCacheElement> 类定义可以用于配置缓存的 [memoryCache](../../../../../docs/framework/configure-apps/file-schema/runtime/memorycache-element-cache-settings.md) 元素。 可以在单个应用程序中使用 <xref:System.Runtime.Caching.MemoryCache> 类的多个实例。 配置文件中的每个 `memoryCache` 元素可以包含一个命名 <xref:System.Runtime.Caching.MemoryCache> 实例的设置。  
  
 \<configuration\>  
\<system.runtime.caching\>  
\<memoryCache\>  
  
## 语法  
  
```  
<memoryCache   
    <namedCaches>  
        <!-- child elements -->  
    </namedCaches>   
< memoryCache />  
```  
  
## 类型  
 <xref:System.Runtime.Caching.MemoryCache> 类。  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`CacheMemoryLimitMegabytes`|<xref:System.Runtime.Caching.MemoryCache> 对象的实例可以增长到的最大内存大小（以兆字节为单位）。 默认值为 0，这意味着默认情况下使用 <xref:System.Runtime.Caching.MemoryCache> 类的自动调整大小启发。|  
|`Name`|缓存配置的名称。|  
|`PhysicalMemoryLimitPercentage`|缓存可以使用的物理内存的百分比。 默认值为 0，这意味着默认情况下使用 <xref:System.Runtime.Caching.MemoryCache> 类的自动调整大小启发。|  
|`PollingInterval`|一个时间间隔的值，在该时间间隔之后，缓存实现会将当前内存负载与为缓存实例设置的基于绝对值和百分比的内存限制进行比较。 该值以“HH:MM:SS”格式输入。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<namedCaches\>](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)|包含 `namedCache` 实例的配置设置的集合。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<system.runtime.caching\>](../../../../../docs/framework/configure-apps/file-schema/runtime/system-runtime-caching-element-cache-settings.md)|包含使你可以在内置到 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 中的应用程序中实现输出缓存的类型。|  
  
## 备注  
 <xref:System.Runtime.Caching.MemoryCache> 类是抽象 <xref:System.Runtime.Caching.ObjectCache> 类的具体实现。<xref:System.Runtime.Caching.MemoryCache> 类的实例可以随来自应用程序配置文件的配置信息一起提供。[memoryCache](../../../../../docs/framework/configure-apps/file-schema/runtime/memorycache-element-cache-settings.md) 配置节包含 `namedCaches` 配置集合。  
  
 基于内存的缓存对象进行初始化时，它首先尝试查找与传递给内存缓存构造函数的参数中的名称进行匹配的 `namedCaches` 项。 如果找到 `namedCaches` 项，则从配置文件检索轮询和内存管理信息。  
  
 初始化过程随后使用构造函数中配置信息的名称\/值对的可选集合来确定是否重写了任何配置项。 如果在名称\/值对集合中传递以下值之一，则这些值会重写从配置文件获取的信息：  
  
-   <xref:System.Runtime.Caching.Configuration.MemoryCacheElement.CacheMemoryLimitMegabytes%2A>  
  
-   <xref:System.Runtime.Caching.Configuration.MemoryCacheElement.PhysicalMemoryLimitPercentage%2A>  
  
-   <xref:System.Runtime.Caching.MemoryCache.PollingInterval%2A>  
  
## 示例  
 下面的示例演示如何通过将 `name` 属性设置为“default”，来将 <xref:System.Runtime.Caching.MemoryCache> 对象的名称设置为默认缓存对象名称。  
  
 将 `cacheMemoryLimitMegabytes` 属性和 `physicalMemoryPercentage` 属性设置为零。 将这些特性设置为零意味着默认情况下使用 <xref:System.Runtime.Caching.MemoryCache> 自动调整大小试探法。 每隔两分钟，缓存实现应对当前内存负载和基于百分比的绝对内存限制进行比较。  
  
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
 <xref:System.Runtime.Caching.MemoryCache>   
 [\<system.runtime.caching\> 元素（缓存设置）](../../../../../docs/framework/configure-apps/file-schema/runtime/system-runtime-caching-element-cache-settings.md)   
 [\<namedCaches\> 元素（缓存设置）](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)