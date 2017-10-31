---
title: "&lt;NetFx40_PInvokeStackResilience&gt; 元素 | Microsoft Docs"
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
  - "<NetFx40_PInvokeStackResilience> 元素"
  - "NetFx40_PInvokeStackResilience 元素"
ms.assetid: 39fb1588-72a4-4479-af74-0605233b68bd
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# &lt;NetFx40_PInvokeStackResilience&gt; 元素
指定运行时是否以降低托管和未托管代码之间的转换速度为代价，自动修复运行时上不正确的平台调用声明。  
  
## 语法  
  
```  
<NetFx40_PInvokeStackResilience  enabled="1|0"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定运行时是否检测不正确的平台调用声明，并在 32 位平台上自动修复运行时上的堆栈。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`0`|运行时使用在 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 中引入的更快的互操作封送处理体系结构，它不会检测和修复不正确的平台调用声明。  这是默认设置。|  
|`1`|运行库使用速度较慢的转换，该转换检测并修复不正确的平台调用声明。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含关于运行时初始化选项的信息。|  
  
## 备注  
 此元素使您用更快的互操作封送处理来交换运行时对不正确的平台调用声明的弹性。  
  
 从 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 开始，简化的互操作封送处理体系结构显著改进了从托管代码到非托管代码的转换的性能。  在早期版本的 .NET Framework 中，封送层对 32 位平台上的不正确平台调用声明进行检测，并自动固定堆栈。  新的封送处理体系结构消除了这一步。  因此，转换速度非常快，但不正确的平台调用声明可能会导致程序故障。  
  
 为了便于在开发过程中检测不正确的声明，对 Visual Studio 调试体验进行了改进。  当您的应用程序在附加调试器的情况下运行时，[pInvokeStackImbalance](../../../../../docs/framework/debug-trace-profile/pinvokestackimbalance-mda.md) 托管调试助手 \(MDA\) 通知您不正确的平台调用声明。  
  
 对于您的应用程序使用不能重编译的组件的地址方案，以及有错误的平台调用声明的地址方案，您可以使用 `NetFx40_PInvokeStackResilience` 元素。  向具有 `enabled="1"` 的应用程序配置文件添加此元素，可以选择采用早期版本的 .NET Framework 行为的兼容性模式，代价是慢速过渡。  已使用 .NET Framework 的早期版本编译的程序集自动选择采用此兼容性模式，而无需此元素。  
  
## 配置文件  
 此元素只可用于应用程序配置文件中。  
  
## 示例  
 下面的示例演示如何以减慢托管和非托管代码间的转换速度为代价，为应用程序选择使用对错误的平台调用声明的更好的弹性。  
  
```  
<configuration>  
   <runtime>  
      <NetFx40_PInvokeStackResilience enabled="1"/>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [pInvokeStackImbalance](../../../../../docs/framework/debug-trace-profile/pinvokestackimbalance-mda.md)