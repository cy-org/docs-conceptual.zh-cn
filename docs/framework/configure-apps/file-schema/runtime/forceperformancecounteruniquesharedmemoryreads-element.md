---
title: "&lt;forcePerformanceCounterUniqueSharedMemoryReads&gt; 元素 | Microsoft Docs"
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
  - "<forcePerformanceCounterUniqueSharedMemoryReads> 元素"
  - "forcePerformanceCounterUniqueSharedMemoryReads 元素"
ms.assetid: 91149858-4810-4f65-9b48-468488172c9b
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# &lt;forcePerformanceCounterUniqueSharedMemoryReads&gt; 元素
指定 PerfCounter.dll 是否在 .NET Framework 1.1 版本的应用程序中使用 CategoryOptions 注册表设置，以决定是否从特定于类别的共享内存或全局内存中加载性能计数器数据。  
  
## 语法  
  
```  
<forcePerformanceCounterUniqueSharedMemoryReads   
enabled="true|false"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指示 PerfCounter.dll 是否使用 CategoryOptions 注册表设置来确定是否从特定于类别的共享内存或全局内存中加载性能计数器数据。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`false`|PerfCounter.dll 不使用该 CategoryOptions 注册表设置，这是默认值。|  
|`true`|PerfCounter.dll 使用该 CategoryOptions 注册表设置。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 在早于 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 的 .NET Framework 版本中，加载的 PerfCounter.dll 版本对应于加载到进程中的运行时。  如果计算机同时安装了 .NET Framework 1.1 版和 [!INCLUDE[dnprdnlong](../../../../../includes/dnprdnlong-md.md)]，则 .NET Framework 1.1 应用程序将加载 PerfCounter.dll 的 .NET Framework 1.1 版。  从 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 开始，加载 PerfCounter.dll 的最新安装版本。  这意味着如果在计算机上安装了 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]，.NET Framework 1.1 应用程序将加的 PerfCounter.dll 的 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 版本。  
  
 从 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 开始，当使用性能计数器时，PerfCounter.dll 为每个提供程序检查 CategoryOptions 注册表项，以决定其应该从特定于分类的共享内存还是从全局共享内存读取。  .NET Framework 1.1 PerfCounter.dll 不读取注册表项，因为它并不知道特定于类别的共享内存；它总是从全局共享内存读取。  
  
 为了向后兼容，当 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] PerfCounter.dll 在 .NET Framework 1.1 应用程序中运行时，将不检查 CategoryOptions 注册表项。  它只使用全局共享内存，如 .NET Framework 1.1 PerfCounter.dll。  但是，通过启用 `<forcePerformanceCounterUniqueSharedMemoryReads>` 元素，您可以指示 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] PerfCounter.dll 检查注册表设置。  
  
> [!NOTE]
>  启用 `<forcePerformanceCounterUniqueSharedMemoryReads>` 元素不保证将使用类别特定的共享内存。  对 `true` 启用的设置仅导致 PerfCounter.dll 引用 CategoryOptions 注册表设置。  CategoryOptions 的默认设置是使用特定于类别的共享内存；但是，您可以更改 CategoryOptions 以指示应使用全局共享的内存。  
  
 包含 CategoryOptions 设置的注册表项是HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\\<categoryName\>\\Performance。  默认情况下，CategoryOptions 设置为 3，指示 PerfCounter.dll 使用类别特定的共享内存。  如果 CategoryOptions 设置为 0，则 PerfCounter.dll 将使用全局共享内存。  仅当正在创建的实例名称与正在重复使用的实例相同时，才可重复使用实例数据。  所有版本都可以写入该类别。  如果 CategoryOptions 设置为 1，则使用全局共享内存，但是，如果类别名称的长度与重复使用的类别名称的长度相同，则可以重复使用实例数据。  
  
 设置 0 和 1 会导致内存泄漏和填满性能计数器内存。  
  
## 示例  
 下面的示例演示如何指定 PerfCounter.dll 应当引用 CategoryOptions 注册表项，以确定它是否应使用特定于类别的共享内存。  
  
```  
<configuration>  
  <runtime>  
    <forcePerformanceCounterUniqueSharedMemoryReads enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)