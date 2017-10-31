---
title: "&lt;performanceCounters&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/performanceCounters"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<perfomanceCounters> 元素"
  - "performanceCounters 元素"
ms.assetid: a71f605b-c7d9-4501-a5c3-abcbb964a43f
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# &lt;performanceCounters&gt; 元素
指定由性能计数器共享的全局内存的大小。  
  
## 语法  
  
```  
<performanceCounters filemappingsize="524288" />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|filemappingsize|必需的特性。<br /><br /> 指定由性能计数器共享的全局内存的大小（以字节为单位）。  默认值为 524288。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`Configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|为 ASP.NET 配置节指定根元素。|  
  
## 备注  
 性能计数器使用内存映射文件或共享内存发布性能数据。共享内存的大小确定一次能够使用多少个实例。存在两种类型的共享内存：全局共享内存和单独的共享内存。全局共享内存由随 .NET Framework 1.0 或 1.1 版一起安装的所有性能计数器类别所使用。随 .NET Framework 2.0 版一起安装的性能计数器类别使用单独的共享内存，每种性能计数器类别拥有自己的内存。  
  
 全局共享内存的大小只能使用配置文件进行设置。默认大小为 524,288 字节，最大大小为 33,554,432 字节，最小大小为 32,768 字节。由于全局共享内存由所有进程和类别共享，第一个创建者将指定大小。如果在应用程序配置文件中定义大小，仅当该应用程序是导致性能计数器执行的第一个应用程序时，才会使用该大小。因此指定 `filemappingsize` 值的正确位置是在 Machine.config 文件中。全局共享内存中的内存不能由单独的性能计数器释放，因此如果创建大量具有不同名称的性能计数器实例，则全局共享内存最终将被耗尽。  
  
 对于单独的共享内存的大小，则首先参考注册表项HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\*\<category name\>*\\Performance中的 DWORD FileMappingSize 值，然后参考配置文件中为全局共享内存指定的值。  如果 FileMappingSize 值不存在，则将单独的共享内存的大小设置为配置文件中的全局设置的四分之一 \(1\/4\)。  
  
## 请参阅  
 <xref:System.Diagnostics.PerformanceCounter>   
 <xref:System.Diagnostics.PerformanceCounterCategory>   
 <xref:System.Diagnostics.PerformanceCounter.InstanceLifetime%2A>   
 <xref:System.Diagnostics.PerformanceCounterInstanceLifetime>