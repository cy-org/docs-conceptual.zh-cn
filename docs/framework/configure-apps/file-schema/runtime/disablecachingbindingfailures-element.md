---
title: "&lt;disableCachingBindingFailures&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#disableCachingBindingFailures"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/disableCachingBindingFailures"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<disableCachingBindingFailures> 元素"
  - "程序集 [.NET Framework], 缓存绑定故障"
  - "缓存程序集绑定故障"
  - "disableCachingBindingFailures 元素"
ms.assetid: bf598873-83b7-48de-8955-00b0504fbad0
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# &lt;disableCachingBindingFailures&gt; 元素
指定当未能通过探测找到程序集时，是否禁用此绑定故障的缓存。  
  
## 语法  
  
```  
<disableCachingBindingFailures enabled="0|1"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|enabled|必需的特性。<br /><br /> 指定当未能通过探测找到程序集时，是否禁用此绑定故障的缓存。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|0|不禁用对绑定故障进行缓存，出现绑定故障是因为通过检测找不到程序集。  这是以 .NET Framework 2.0 版开头的默认绑定行为。|  
|1|禁用对绑定故障进行缓存，出现绑定故障是因为通过探测找不到程序集。  这一设置将恢复为 .NET Framework 1.1 版的绑定行为。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 从 .NET Framework 2.0 版开始中，载入程序集时的默认行为是对所有绑定和载入故障进行缓存。  即，如果尝试加载程序集失败，则对于同一程序集的后续请求将立即失败，而不会进行任何尝试来定位该程序集。  此元素禁用由于未能在探测路径中找到程序集而出现绑定故障时，绑定故障的默认行为。  这些故障会引发 <xref:System.IO.FileNotFoundException>。  
  
 一些绑定和加载故障不会受此元素影响，并始终缓存。  出现这些故障是因为程序集已找到，但未能加载。  它们引发 <xref:System.BadImageFormatException> 或 <xref:System.IO.FileLoadException>。  下面的列表包含此类故障的一些示例。  
  
-   如果尝试加载一个不是有效的程序集文件，则即使用正确的文件将错误的文件替换，加载程序集的后续尝试也将失败。  
  
-   如果尝试加载一个被文件系统锁定的程序集，则即使在文件系统将程序集释放之后，加载程序集的后续尝试也将失败。  
  
-   如果您正在尝试加载的一个或多个版本的程序集位于探测路径中，但您请求的特定版本不在其中，则即使正确的版本被移动到探测路径中，加载该版本的后续尝试也将失败。  
  
## 示例  
 下面的代码示例示出了如何禁用程序集绑定故障的缓存，改故障因为通过探测找不到程序集而发生。  
  
```  
<configuration>  
   <runtime>  
      <disableCachingBindingFailures enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [运行时如何定位程序集](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)