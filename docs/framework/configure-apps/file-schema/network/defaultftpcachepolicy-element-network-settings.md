---
title: "&lt;defaultFtpCachePolicy&gt; 元素（网络设置） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultFtpCachePolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching/defaultFtpCachePolicy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<defaultFtpCachePolicy> 元素"
  - "defaultFtpCachePolicy 元素"
ms.assetid: 0eb0c5cb-dd97-484d-8614-785e88877abb
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# &lt;defaultFtpCachePolicy&gt; 元素（网络设置）
描述 FTP 缓存功能是否处于活动状态并描述默认缓存策略。  
  
## 语法  
  
```  
< defaultFtpCachePolicy  
  policyLevel="BypassCache|Default|CacheOnly|CacheIfAvailable|Revalidate|Reload|NoCacheNoStore|Revalidate"  
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`policyLevel`|指定 FTP 缓存策略。  默认值为 `Default`。|  
  
## policyLevel 特性  
  
|值|说明|  
|-------|--------|  
|`Default`|如果缓存的资源是新的，内容长度准确，并且具有过期、修改和内容长度特性，则返回缓存的资源。|  
|`BypassCache`|从服务器返回资源。|  
|`CacheOnly`|如果内容长度存在并与项大小匹配，将返回缓存的资源。|  
|`CacheIfAvailable`|如果提供了内容长度并且与项大小匹配，则返回缓存的资源；否则从服务器下载该资源并将其返回给调用方。|  
|`Revalidate`|如果缓存资源的时间戳与服务器上的资源的时间戳相同，将返回缓存的资源；否则，从服务器下载资源，将其存储在缓存中并返回给调用方。|  
|`Reload`|从服务器下载资源，将其存储在缓存中并返回给调用方。|  
|`NoCacheNoStore`|如果存在缓存的资源，则将其删除。  从服务器下载资源并将其返回给调用方。|  
|`Revalidate`|如果时间戳与服务器上的资源的时间戳相同，则使用资源的缓存副本满足请求；否则从服务器下载资源，将资源展示给调用方然后存储在缓存中。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[requestCaching](../../../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)|控制网络请求的缓存机制。|  
  
## 备注  
  
## 示例  
 下面的代码示例演示如何指定 `NoCacheNoStore` 的 FTP 缓存策略。  
  
```  
<configuration>  
  <system.net>  
    <requestCaching>  
      <defaultFtpCachePolicy  
        Level="NoCacheNoStore">  
      </defaultFtpCachePolicy>  
    </requestCaching>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.Cache>   
 <xref:System.Net.WebRequest>   
 <xref:System.Net.Cache.RequestCacheLevel>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)