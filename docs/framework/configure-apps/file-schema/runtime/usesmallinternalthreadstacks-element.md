---
title: "&lt;UseSmallInternalThreadStacks&gt; 元素 | Microsoft Docs"
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
  - "<UseSmallInternalThreadStacks> 元素"
  - "UseSmallInternalThreadStacks 元素"
ms.assetid: 1e3f6ec0-1cac-4e1c-9c81-17d948ae5874
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# &lt;UseSmallInternalThreadStacks&gt; 元素
请求公共语言运行库 \(CLR\) 减少内存使用，方法是在其创建内部使用的特定线程时指定堆栈大小，而不是使用那些线程的默认堆栈大小。  
  
## 语法  
  
```  
<UseSmallInternalThreadStacks enabled="true|false" />  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|enabled|必需的特性。<br /><br /> 指定是否求的 CLR 使用显式的堆栈大小而不是默认堆栈大小，前提是它创建在内部使用的特定线程时。  显式的堆栈大小都小于 1 MB 的默认堆栈大小。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|true|请求显式堆栈大小。|  
|false|使用默认堆栈大小。  这是 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 的默认值。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 此配置元素用来请求在一个过程中的减少虚拟内存的使用，因为如果请求生效，CLR 对其内部的线程使用的显式线程大小都小于默认大小。  
  
> [!IMPORTANT]
>  此配置元素是一个 CLR 请求，而不是绝对的请求。  在 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]，请求仅遵守 x 86 体系结构。  此元素可能在将来的 CLR 版本中被完全忽略或被始终用于选定的内部线程的显式堆栈大小替换。  
  
 如果 CLR 接受请求，指定此配置元素交易的可靠性，因为较小的堆栈大小可能会使堆栈更有可能溢出。  
  
## 示例  
 下面的示例说明如何请求 CLR 使用显式堆栈大小，用于某些在内部使用的线程。  
  
```  
<configuration>  
   <runtime>  
      <UseSmallInternalThreadStacks enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)