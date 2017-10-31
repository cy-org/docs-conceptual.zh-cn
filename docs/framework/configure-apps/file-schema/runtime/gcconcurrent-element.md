---
title: "&lt;gcConcurrent&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/gcConcurrent"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#gcConcurrent"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<gcConcurrent> 元素"
  - "容器标记, <gcConcurrent> 元素"
  - "gcConcurrent 元素"
ms.assetid: 503f55ba-26ed-45ac-a2ea-caf994da04cd
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# &lt;gcConcurrent&gt; 元素
指定公共语言运行时是否在单独线程上运行垃圾回收。  
  
## 语法  
  
```  
<gcConcurrent    
   enabled="true|false"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定运行时是否并发运行服务器垃圾回收。|  
  
## enabled 特性  
  
|值|描述|  
|-------|--------|  
|`false`|不并发运行垃圾回收。|  
|`true`|并发运行垃圾回收。  这是默认设置。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 在.NET Framework 4 之前，工作站垃圾回收支持并发垃圾回收，在后台对一个单独线程执行垃圾回收。  在.NET Framework 4 中，并发垃圾回收被后台 GC 取代，它还在单独的线程上在后台中执行垃圾回收。  从 .NET Framework 4.5 开始，服务器垃圾回收可提供后台垃圾回收。  `<gcConcurrent>` 元素控制运行时是执行并发还是后台垃圾回收（如果可行），或者是否在前台执行垃圾回收。  
  
> [!WARNING]
>  从.NET Framework 4 开始，并发垃圾回收替换为后台垃圾回收。  *并发*和*后台*条款可在 .NET Framework 文档中互换使用。  若要禁用后台垃圾回收，请使用 `<gcConcurrent>` 元素，如本文所述。  
  
 默认情况下，运行时使用并发或后台垃圾回收，回收针对延迟进行了优化。  如果应用程序涉及大量用户交互，则通过让并发垃圾回收保持启用状态，可最大限度缩短应用程序执行垃圾回收时的暂停时间。  如果将 `enabled` 元素的 `<gcConcurrent>` 特性设置为 `false`，运行时将使用针对吞吐量优化的非并发垃圾回收。  下列配置文件会禁用后台垃圾回收。  
  
```xml  
  
<configuration>  
   <runtime>  
      <gcConcurrent enabled="false"/>  
   </runtime>  
</configuration>  
  
```  
  
 如果计算机配置文件中有 `<gcConcurrentSetting>` 设置，它会为所有 .NET Framework 应用程序定义默认值。  计算机配置文件设置将重写应用程序配置文件设置。  
  
 有关并发和后台垃圾回收的详细信息，请参阅[Fundamentals of Garbage Collection](../../../../../docs/standard/garbage-collection/fundamentals.md)主题中的“并发垃圾回收”一节。  
  
## 示例  
 下列示例启用并发垃圾回收。  
  
```  
  
<configuration>  
   <runtime>  
      <gcConcurrent enabled="true"/>  
   </runtime>  
</configuration>  
  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Fundamentals of Garbage Collection](../../../../../docs/standard/garbage-collection/fundamentals.md)