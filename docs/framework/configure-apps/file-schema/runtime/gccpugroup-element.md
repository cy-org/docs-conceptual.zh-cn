---
title: "&lt;GCCpuGroup&gt; 元素 | Microsoft Docs"
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
  - "<GCCpuGroup> 元素"
  - "GCCpuGroup 元素"
ms.assetid: c1fc7d6c-7220-475c-a312-5b8b201f66e0
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# &lt;GCCpuGroup&gt; 元素
指定垃圾回收是否支持多个 CPU 组。  
  
## 语法  
  
```  
<GCCpuGroup    
   enabled="true|false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定垃圾回收是否支持多个 CPU 组。|  
  
## enabled 特性  
  
|值|描述|  
|-------|--------|  
|`false`|垃圾回收不支持多个 CPU 组。  这是默认值。|  
|`true`|如果服务器垃圾回收启用，垃圾回收支持多个 CPU 组。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 当计算机具有多个 CPU 组，并服务器垃圾回收启用 \(请参见 [\<gcServer\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gcserver-element.md) 元素\)，在创建和平衡堆时启用此元素扩展在所有 CPU 团队中的垃圾回收并回收所有核心。  
  
> [!NOTE]
>  此元素仅适用于垃圾回收线程。  若要启用运行时分配所有CPU 组中的用户线程，还必须启用 [\<Thread\_UseAllCpuGroups\>](../../../../../docs/framework/configure-apps/file-schema/runtime/thread-useallcpugroups-element.md) 元素。  
  
## 示例  
 下面的示例演示了如何启用对多个 CPU 组的垃圾回收。  
  
```  
<configuration>  
   <runtime>  
      <GCCpuGroup enabled="true"/>  
      <gcServer enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [How to: Disable Concurrent Garbage Collection](http://msdn.microsoft.com/zh-cn/ba2c6c67-5778-497c-9fac-5f793b5500c7)   
 [工作站和服务器垃圾回收](../../../../../docs/standard/garbage-collection/fundamentals.md#workstation_and_server_garbage_collection)