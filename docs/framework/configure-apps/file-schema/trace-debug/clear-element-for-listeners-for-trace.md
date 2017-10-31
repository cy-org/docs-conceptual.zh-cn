---
title: "&lt;trace&gt; 的 &lt;listeners&gt; 的 &lt;clear&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/clear"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<trace> 的 <listeners> 的 <clear> 元素"
  - "<trace> 的 <listeners> 的 clear 元素"
ms.assetid: b44732a8-271f-4a06-ba9e-fe3298d6f192
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# &lt;trace&gt; 的 &lt;listeners&gt; 的 &lt;clear&gt; 元素
清除跟踪的 `Listeners` 集合。  
  
## 语法  
  
```  
<clear/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。|  
|`trace`|包含对跟踪消息进行收集、存储和路由的侦听器。|  
|`listeners`|包含对消息进行收集、存储和路由的侦听器。  侦听器将跟踪输出定向到合适的目标。|  
  
## 备注  
 `<clear>` 元素从跟踪的 `Listeners` 集合中移除所有侦听器。  在使用 `<add>` 元素之前，可以使用 `<clear>` 元素确认该集合中没有其他活动的侦听器。  
  
 通过对 <xref:System.Diagnostics.Trace.Listeners%2A?displayProperty=fullName> 属性调用 <xref:System.Diagnostics.TraceListenerCollection.Clear%2A> 方法 \(`System.Diagnostics.Trace.Listeners.Clear()`\)，可以通过编程方式清除 `Listeners` 集合。  
  
 此元素可用于计算机配置文件 \(Machine.config\) 和应用程序配置文件。  
  
> [!NOTE]
>  `<clear>` 元素从 `Listeners` 集合中移除 <xref:System.Diagnostics.DefaultTraceListener>，更改 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>、<xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>、<xref:System.Diagnostics.Debug.Fail%2A?displayProperty=fullName> 和 <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=fullName> 方法的行为。  调用 `Assert` 或 `Fail` 方法通常会显示一个消息框。  但是，如果 <xref:System.Diagnostics.DefaultTraceListener> 不在 `Listeners` 集合中，则不会显示消息框。  
  
## 示例  
 下面的示例演示如何在使用 `<add>` 元素将侦听器 `console` 添加到跟踪的 `Listeners` 集合之前使用 `<clear>` 元素。  
  
```  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="false" indentsize="4">  
      <listeners>  
        <clear/>  
        <add name="console"   
          type="System.Diagnostics.ConsoleTraceListener" >  
          <filter type="System.Diagnostics.EventTypeFilter"   
            initializeData="Error" />  
        </add>  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>   
```  
  
## 请参阅  
 <xref:System.Diagnostics.Trace.Listeners%2A>   
 <xref:System.Diagnostics.Trace>   
 <xref:System.Diagnostics.Debug>   
 <xref:System.Diagnostics.TraceSource>   
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)   
 [\<remove\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/remove-element-for-listeners-for-trace.md)   
 [Trace Listeners](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)