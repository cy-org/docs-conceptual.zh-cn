---
title: "&lt;sharedListeners&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#sharedListeners"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<sharedListeners> 元素"
  - "侦听器"
  - "共享侦听器"
  - "sharedListeners 元素"
  - "跟踪侦听器, <sharedListeners> 元素"
ms.assetid: de200534-19dd-4156-86cf-c50521802c4c
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# &lt;sharedListeners&gt; 元素
包含任何源或跟踪元素都能引用的侦听器。这些侦听器默认不接收任何跟踪，并且也不可能在运行时检索这些侦听器。  标识为共享侦听器的侦听器可按名称添加到源或跟踪。  
  
## 语法  
  
```  
<sharedListeners>   
  <add>...</add>  
</sharedListeners>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/add-element-for-listeners-for-trace.md)|将侦听器添加到 `sharedListeners` 集合中。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`Configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|为 ASP.NET 配置节指定根元素。|  
  
## 备注  
 向共享侦听器集合添加侦听器不会使它成为活动侦听器。  仍需将它添加到跟踪源或跟踪，方法是将它添加到跟踪元素的 `Listeners` 集合。  .NET Framework 中的侦听器类从 <xref:System.Diagnostics.TraceListener> 类派生。  
  
 此元素可用于计算机配置文件 \(Machine.config\) 和应用程序配置文件。  
  
## 示例  
 下面的示例演示如何使用 `<sharedListeners>` 元素将侦听器 `console` 添加到 <xref:System.Diagnostics.TraceSource> 和 <xref:System.Diagnostics.Trace> 类的 `Listeners` 集合中。  控制台跟踪侦听器通过调用 <xref:System.Diagnostics.TraceSource> 或 <xref:System.Diagnostics.Trace> 将跟踪信息写到控制台。  
  
```  
<configuration>  
  <system.diagnostics>  
    <sharedListeners>  
      <add name="console" type="System.Diagnostics.ConsoleTraceListener" >  
        <filter type="System.Diagnostics.EventTypeFilter"  
          initializeData="Warning" />  
      </add>  
    </sharedListeners>  
    <sources>  
      <source name="mySource" switchName="sourceSwitch"  >  
        <listeners>  
          <add name="console" />  
        </listeners>  
      </source>  
    </sources>  
    <switches>  
      <add name="sourceSwitch" value="Verbose"/>  
    </switches>  
    <trace>  
      <listeners>  
        <add name="console" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration></system.diagnostics>   
```  
  
## 请参阅  
 <xref:System.Diagnostics.TraceListener>   
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)   
 [Trace Listeners](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)