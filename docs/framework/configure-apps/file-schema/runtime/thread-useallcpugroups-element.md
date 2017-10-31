---
title: "&lt;Thread_UseAllCpuGroups&gt; 元素 | Microsoft Docs"
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
ms.assetid: d30fe7c5-8469-46e2-b804-e3eec7b24256
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# &lt;Thread_UseAllCpuGroups&gt; 元素
指定运行时是否在所有的 CPU 组中分布托管的线程。  
  
## 语法  
  
```vb  
<Thread_UseAllCpuGroups    
   enabled="true|false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定运行时是否在所有的 CPU 组中分布托管的线程。|  
  
## enabled 特性  
  
|值|描述|  
|-------|--------|  
|`false`|运行时不会跨多个 CPU 组分发托管线程。  这是默认设置。|  
|`true`|如果计算机具有多个 CPU 组，并 [\<GCCpuGroup\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md) 元素已启用，运行时在多个 CPU 组中分布托管线程。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 当计算机具有多个 CPU 组时，启用此元素会导致运行时在所有 CPU 组中分发托管线程。  若要使用此功能，您还必须启用 [\<GCCpuGroup\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md) 元素，这种元素可以将垃圾回收扩展至所有 CPU 组，并在创建和平衡堆时将考虑所有内核。  启用 [\<GCCpuGroup\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md) 组件需要启用 [\<gcServer\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gcserver-element.md) 元素。  如果这些元素未启用，则启用 `<Thread_UseAllCpuGroups>` 元素将无作用。  
  
## 示例  
 下面的示例演示了如何启用对多个 CPU 组的支持。  
  
```  
<configuration>  
   <runtime>  
      <Thread_UseAllCpuGroups enabled="true"/>  
      <GCCpuGroup enabled="true"/>  
      <gcServer enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<GCCpuGroup\> 元素](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md)