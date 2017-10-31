---
title: "&lt;requestCaching&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#requestCaching"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<requestCaching> 元素"
  - "requestCaching 元素"
ms.assetid: 9962a2fe-cbda-41a6-9377-571811eaea84
caps.latest.revision: 20
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 20
---
# &lt;requestCaching&gt; 元素（网络设置）
控制网络请求的缓存机制。  
  
## 语法  
  
```  
  
      <requestCaching  
  isPrivateCache ="true|false"  
  disableAllCaching="true|false"  
  defaultPolicyLevel="BypassCache|Default|CacheOnly|CacheIfAvailable|Revalidate|Reload|NoCacheNoStore|Revalidate"  
  unspecifiedMaximumAge= "d.hh.mm.ss""  
  <defaultHttpCachePolicy> … </defaultHttpCachePolicy>  
  <defaultFtpCachePolicy> … </defaultFtpCachePolicy>  
/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`isPrivateCache`|指定进行缓存时是否在不同用户的信息之间提供隔离。  默认值为 `true`。  对于中间层应用程序，该值应当为 `false`。|  
|`disableAllCaching`|指定对所有 Web 响应禁用缓存，且不能以编程方式重写此设置。|  
|`defaultPolicyLevel`|<xref:System.Net.Cache.RequestCacheLevel> 枚举中的一个值。  默认值为 `BypassCache`。|  
|`unspecifiedMaximumAge`|指定默认时间，在该时间之后内容将标记为过期。|  
  
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
|`Revalidate`|如果时间戳与服务器上的资源的时间戳相同，将通过使用资源的缓存副本来满足请求；否则，从服务器下载资源，将其提供给调用方并存储在缓存中。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[defaultHttpCachePolicy](../../../../../docs/framework/configure-apps/file-schema/network/defaulthttpcachepolicy-element-network-settings.md)|可选元素。<br /><br /> 描述 HTTP 缓存功能是否处于活动状态并描述默认的缓存策略。|  
|[\<defaultFtpCachePolicy\> 元素（网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/defaultftpcachepolicy-element-network-settings.md)|可选元素。<br /><br /> 描述 FTP 缓存功能是否处于活动状态并描述默认缓存策略。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[system.net](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)|包含指定 .NET Framework 与网络的连接方式的设置。|  
  
## 示例  
 下面的代码示例演示如何禁用所有缓存。  
  
```  
<configuration>  
  <system.net>  
    <requestCaching  
      disableAllCaching="true"  
    />  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.Cache?displayProperty=fullName>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)