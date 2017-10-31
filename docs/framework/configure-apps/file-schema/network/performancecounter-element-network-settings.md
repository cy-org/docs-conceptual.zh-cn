---
title: "&lt;performanceCounter&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/performanceCounters"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<performanceCounter> 元素"
  - "performanceCounter 元素"
ms.assetid: 3afa1586-e1b8-473d-8985-c3fc90cf561b
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# &lt;performanceCounter&gt; 元素（网络设置）
启用或禁用网络性能计数器。  
  
## 语法  
  
```  
<performanceCounters  
  enabled="true|false"  
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|指定是否启用网络性能计数器。  默认值为 `false`。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[设置](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|配置 <xref:System.Net> 命名空间的基本网络选项。|  
  
## 备注  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
 需要在要使用的配置文件中启用网络性能计数器。  使用配置文件中的单个设置启用或禁用所有网络性能计数器。  无法启用或禁用单个网络性能计数器。  有关特定网络性能计数器的更多信息，请参见[Networking Performance Counters](http://msdn.microsoft.com/zh-cn/d1860235-f643-46ae-846c-ff0ed8b0e3cd)。  
  
 默认值是禁用网络性能计数器。  
  
 <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=fullName> 属性可用于从适用的配置文件获取 **enabled** 特性的当前值。  
  
## 示例  
 下面的代码示例演示如何配置 <xref:System.Net> 和相关命名空间以启用网络性能计数器。  
  
```  
<configuration>  
  <system.net>  
    <settings>  
      <performanceCounters  
        enabled="true"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.Configuration.PerformanceCountersElement?displayProperty=fullName>   
 <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=fullName>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)   
 [Networking Performance Counters](http://msdn.microsoft.com/zh-cn/d1860235-f643-46ae-846c-ff0ed8b0e3cd)