---
title: "&lt;source&gt; 的 &lt;listeners&gt; 的 &lt;remove&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<source> 的 <listeners> 的 <remove> 元素"
  - "<source> 的 <listeners> 的 remove 元素"
ms.assetid: 3ff6b578-273d-407f-b07f-8251f1f9f5d0
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# &lt;source&gt; 的 &lt;listeners&gt; 的 &lt;remove&gt; 元素
从跟踪源的 `Listeners` 集合中移除侦听器。  
  
## 语法  
  
```  
<remove name="listenerName" />  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`name`|必需的特性。<br /><br /> 要从 `Listeners` 集合中移除的侦听器的名称。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。|  
|`sources`|包含启动跟踪消息的跟踪源。|  
|`source`|指定启动跟踪消息的跟踪源。|  
|`listeners`|指定对消息进行收集、存储和路由的侦听器。|  
  
## 备注  
 `<remove>` 元素从跟踪源的 `Listeners` 集合中移除指定的侦听器。  
  
 通过调用 <xref:System.Diagnostics.TraceSource> 实例的 <xref:System.Diagnostics.TraceSource.Listeners%2A> 属性上的 <xref:System.Diagnostics.TraceListenerCollection.Remove%2A> 方法，可以以编程方式从跟踪源的 `Listeners` 集合中移除元素。  
  
 此元素可用于计算机配置文件 \(Machine.config\) 和应用程序配置文件。  
  
## 示例  
 下面的示例演示如何在使用 `<add>` 元素将侦听器 `console` 添加到跟踪源 `TraceSourceApp` 的 `Listeners` 集合之前使用 `<remove>` 元素。  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="TraceSourceApp" switchName="sourceSwitch"   
         switchType="System.Diagnostics.SourceSwitch" >  
         <listeners>  
           <remove name="Default"/>  
           <add name="console"   
             type="System.Diagnostics.ConsoleTraceListener" />  
         </listeners>  
      </source>  
    </sources>  
  </system.diagnostics>  
</configuration>   
```  
  
## 请参阅  
 <xref:System.Diagnostics.TraceSource.Listeners%2A>   
 <xref:System.Diagnostics.TraceSource>   
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)   
 [\<clear\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/clear-element-for-listeners-for-source.md)   
 [Trace Listeners](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)