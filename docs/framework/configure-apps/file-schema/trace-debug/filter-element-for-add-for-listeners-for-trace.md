---
title: "&lt;trace&gt; 的 &lt;listeners&gt; 的 &lt;add&gt; 的 &lt;filter&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/add/filter"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<trace> 的 <listeners> 的 <add> 的 <filter> 元素"
  - "<trace> 的 <listeners> 的 <add> 的 filter 元素"
  - "initializeData 特性"
ms.assetid: eb9c18f5-dfa8-47c5-b91b-e4b93e76e1cc
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# &lt;trace&gt; 的 &lt;listeners&gt; 的 &lt;add&gt; 的 &lt;filter&gt; 元素
向跟踪的 `Listeners` 集合中的侦听器添加筛选器。  
  
## 语法  
  
```  
<filter   
  type="traceFilterClassName"   
  initializeData="data" />  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`type`|必需的特性。<br /><br /> 指定筛选器的类型，该类型应该从 <xref:System.Diagnostics.TraceFilter> 类继承。  可以使用以命名空间限定的类型名称，它对应于类型的 <xref:System.Type.FullName%2A> 属性，或者可以使用包括程序集信息的完全限定的类型名称，它对应于 <xref:System.Type.AssemblyQualifiedName%2A> 属性。  有关完全限定的类型名称的信息，请参见 [指定完全限定的类型名称](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)。|  
|`initializeData`|可选特性。<br /><br /> 传递到指定筛选类的构造函数的字符串。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。|  
|`trace`|包含对跟踪消息进行收集、存储和路由的侦听器。|  
|`listeners`|包含对消息进行收集、存储和路由的侦听器。  侦听器将跟踪输出定向到合适的目标。|  
|`add`|将侦听器添加到 `Listeners` 集合中。|  
  
## 备注  
 `<filter>` 元素必须包含在跟踪侦听器的 `<add>` 元素中，该元素指定侦听器的类型而不只是 [\<sharedListeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sharedlisteners-element.md) 中定义的侦听器的名称。  如果 [\<sharedListeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sharedlisteners-element.md) 中定义了侦听器，则必须在该元素中定义侦听器的筛选器。  
  
 此元素可用于计算机配置文件 \(Machine.config\) 和应用程序配置文件。  
  
## 示例  
 下面的示例演示如何使用 `<filter>` 元素向跟踪的 `Listeners` 集合中的侦听器 `console` 添加筛选器，并将筛选器事件级别指定为 `Error`。  
  
```  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="false" indentsize="4">  
      <listeners>  
        <add name="console"   
          type="System.Diagnostics.ConsoleTraceListener" >  
          <filter type="System.Diagnostics.EventTypeFilter"   
            initializeData="Error" />  
        </add>  
        <remove name="Default" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Diagnostics.Trace>   
 <xref:System.Diagnostics.TraceListener>   
 <xref:System.Diagnostics.TraceListener.Filter%2A?displayProperty=fullName>   
 <xref:System.Diagnostics.TraceFilter>   
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)