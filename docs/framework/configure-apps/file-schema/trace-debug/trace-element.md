---
title: "&lt;trace&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#trace"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<trace> 元素"
  - "侦听器"
  - "trace 元素"
  - "跟踪侦听器, <trace> 元素"
ms.assetid: 7931c942-63c1-47c3-a045-9d9de3cacdbf
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# &lt;trace&gt; 元素
包含对跟踪消息进行收集、存储和路由的侦听器。  
  
## 语法  
  
```  
<trace autoflush="true|false"   
       indentsize="indent value"  
       useGlobalLock="true| false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`autoflush`|可选特性。<br /><br /> 指定跟踪侦听器是否在每次写入操作后自动刷新输出缓冲区。|  
|`indentsize`|可选特性。<br /><br /> 指定要缩进的空格数。|  
|`useGlobalLock`|可选特性。<br /><br /> 指示是否应使用全局锁。|  
  
## autoflush 特性  
  
|值|说明|  
|-------|--------|  
|`false`|不自动刷新输出缓冲区。  这是默认值。|  
|`true`|自动刷新输出缓冲区。|  
  
## useGlobalLock 特性  
  
|值|说明|  
|-------|--------|  
|`false`|如果侦听器是线程安全的，则不使用全局锁；否则使用全局锁。|  
|`true`|始终使用全局锁，无论侦听器是否为线程安全的。  这是默认值。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<listeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/listeners-element-for-trace.md)|指定对消息进行收集、存储和路由的侦听器。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。|  
  
## 示例  
 下面的示例演示如何使用 `<trace>` 元素将侦听器 `MyListener` 添加到 `Listeners` 集合。  `MyListener` 创建一个名为 `MyListener.log` 的文件，并将输出写入到该文件。  `useGlobalLock` 特性设置为 `false`，这导致在跟踪侦听器是线程安全的情况下不使用全局锁。  `autoflush` 特性设置为 `true`，这导致无论是否调用 <xref:System.Diagnostics.Trace.Flush%2A?displayProperty=fullName> 方法，跟踪侦听器都将写入该文件。  `indentsize` 特性设置为 0（零），这导致在调用 <xref:System.Diagnostics.Trace.Indent%2A?displayProperty=fullName> 方法时，侦听器不缩进（缩进的空格数为零）。  
  
```  
<configuration>  
   <system.diagnostics>  
      <trace useGlobalLock="false" autoflush="true" indentsize="0">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Diagnostics.TraceListener>   
 <xref:System.Diagnostics.DefaultTraceListener>   
 <xref:System.Diagnostics.TextWriterTraceListener>   
 <xref:System.Diagnostics.EventLogTraceListener>   
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)