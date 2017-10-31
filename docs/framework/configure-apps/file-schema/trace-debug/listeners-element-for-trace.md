---
title: "&lt;trace&gt; 的 &lt;listeners&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<listeners> 元素"
  - "listeners 元素"
ms.assetid: 1394c2c3-6304-46db-87c1-8e8b16f5ad5b
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 17
---
# &lt;trace&gt; 的 &lt;listeners&gt; 元素
指定对消息进行收集、存储和路由的侦听器。  侦听器将跟踪输出定向到合适的目标。  
  
## 语法  
  
```  
<listeners>   
  <add>...</add>  
  <clear/>  
  <remove ... />  
</listeners>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/add-element-for-listeners-for-trace.md)|将侦听器添加到 `Listeners` 集合中。|  
|[\<clear\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/clear-element-for-listeners-for-trace.md)|清除跟踪的 `Listeners` 集合。|  
|[\<remove\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/remove-element-for-listeners-for-trace.md)|从 `Listeners` 集合中移除侦听器。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|为 ASP.NET 配置节指定根元素。|  
|`trace`|包含对跟踪消息进行收集、存储和路由的侦听器。|  
  
## 备注  
 <xref:System.Diagnostics.Debug> 和 <xref:System.Diagnostics.Trace> 类共享同一个 **Listeners** 集合。  如果将侦听器对象添加到其中一个类的集合中，其他类则会使用相同的侦听器。  随 .NET Framework 一起提供的侦听器类从 <xref:System.Diagnostics.TraceListener> 类派生。  
  
## 配置文件  
 此元素可用于计算机配置文件 \(Machine.config\) 和应用程序配置文件。  
  
## 示例  
 下面的示例演示如何使用 **\<listeners\>**元素将侦听器 `MyListener`和`MyEventListener` 添加到 **Listeners**集合。  `MyListener` 创建一个名为 `MyListener.log` 的文件，并将输出写入到该文件。  `MyEventListener` 在事件日志中创建一项。  
  
```  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="true" indentsize="0">  
      <listeners>  
        <add name="myListener"   
          type="System.Diagnostics.TextWriterTraceListener,   
            system, version=1.0.3300.0, Culture=neutral,   
            PublicKeyToken=b77a5c561934e089"   
          initializeData="c:\myListener.log" />  
        <add name="MyEventListener"  
          type="System.Diagnostics.EventLogTraceListener,   
            system, version=1.0.3300.0, Culture=neutral,   
            PublicKeyToken=b77a5c561934e089"  
          initializeData="MyConfigEventLog"/>  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Diagnostics.TraceListener>   
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)