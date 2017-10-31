---
title: "&lt;defaultHttpCachePolicy&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching/defaultHttpCachePolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultHttpCachePolicy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<defaultHttpCachePolicy> 元素"
  - "defaultHttpCachePolicy 元素"
ms.assetid: 2c1247d0-39b0-4c12-919a-a925ce075c79
caps.latest.revision: 19
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 19
---
# &lt;defaultHttpCachePolicy&gt; 元素（网络设置）
描述 HTTP 缓存功能是否处于活动状态并描述默认的缓存策略。  
  
## 语法  
  
```  
< defaultHttpCachePolicy  
  policyLevel="BypassCache|Default"  
  minimumFresh="d.hh:mm:ss"|"minValue"  
  maximumAge  ="d.hh:mm:ss"|"maxValue"  
  maximumStale="d.hh:mm:ss"|"maxValue"  
/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`maximumAge`|指定在将缓存的对象标记为过期之前的最长时间间隔。|  
|`maximumStale`|指定在计算出的新鲜时间过期之后可经过的最长时间，超过此时间之后，会将缓存的对象标记为已过期。|  
|`minimumFresh`|指定缓存的对象被视为新鲜的最短时间。|  
|`policyLevel`|指定缓存策略是否为自动策略或者是否忽略缓存。  默认值为 `BypassCache`。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[请求缓存](../../../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)|控制网络请求的缓存机制。|  
  
## 备注  
 `policyLevel` 特性的值为 `BypassCache` 或 `Default`。  
  
 `maximumAge`, `maximumStale`，和`minimumFresh`元素的值，是显示的时间间隔，该时间间隔以*d*.*hh*:*mm*:*ss* \(天，时， 分， 和秒\), 或者不变的 `minValue` 或者 `maxValue`为格式，如适当的。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例演示如何将最短新鲜时间指定为六个小时、将最长生存期指定为两天，以及将最长陈旧时间指定为四个小时。  
  
```  
<configuration>  
  <system.net>  
    <requestCaching>  
      <defaultHttpCachePolicy>  
        <set minimumFresh="0.06:00:00" />  
        <set maximumAge  ="2.00:00:00" />  
        <set maximumStale="0.04:00:00" />  
      </defaultHttpCachePolicy>  
    </requestCaching>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.Cache>   
 <xref:System.Net.WebRequest>   
 <xref:System.Net.Cache.RequestCacheLevel>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)