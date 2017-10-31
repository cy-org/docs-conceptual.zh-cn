---
title: "&lt;sharedListeners&gt; 的 &lt;add&gt; 的 &lt;filter&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners/add/filter"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<sharedListeners> 的 <add> 的 <filter> 元素"
  - "<sharedListeners> 的 <add> 的 filter 元素"
  - "筛选器, 跟踪侦听器"
  - "initializeData 特性"
  - "跟踪侦听器, 筛选器"
ms.assetid: 7d4e7faa-2e4e-4379-ac76-f6cd7f2f8fac
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# &lt;sharedListeners&gt; 的 &lt;add&gt; 的 &lt;filter&gt; 元素
向 `sharedListeners` 集合中的侦听器添加筛选器。  
  
## 语法  
  
```  
<filter type="System.Diagnostics.EventTypeFilter"   
  initializeData="Warning" />  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|**type**|必需的特性。<br /><br /> 指定筛选器的类型。  可以只使用类型的完整名称（以 <xref:System.Type.FullName%2A?displayProperty=fullName> 属性的格式），也可以使用包括程序集信息的完全限定的类型名称（以 <xref:System.Type.AssemblyQualifiedName%2A?displayProperty=fullName> 属性的格式）。  有关创建完全限定的类型名称的信息，请参见 [指定完全限定的类型名称](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)。|  
|**initializeData**|可选特性。<br /><br /> 传递到指定类的构造函数的字符串。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。|  
|`sharedListeners`|任何源或跟踪元素都能引用的侦听器的集合。|  
|`add`|将侦听器添加到 **sharedListeners** 集合中。|  
  
## 备注  
 如果 `<sharedListeners>` 元素的 `<add>` 元素中定义了某个侦听器，则应该在属于 `<add>` 元素的子元素的 `<filter>` 元素中定义该侦听器的筛选器。  
  
 此元素可用于计算机配置文件 \(Machine.config\) 和应用程序配置文件。  
  
## 示例  
 下面的示例演示如何使用 `<filter>` 元素向 `sharedListeners` 集合中的跟踪侦听器 `console` 添加筛选器。  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="myTraceSource" >  
        <listeners>  
          <add name="console" />  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="console"   
        type="System.Diagnostics.ConsoleTraceListener" >  
        <filter type="System.Diagnostics.EventTypeFilter"   
          initializeData="Error" />  
      </add>  
    </sharedListeners>  
  </system.diagnostics>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Diagnostics.TraceFilter>   
 <xref:System.Diagnostics.TraceListener>   
 <xref:System.Diagnostics.TraceSource>   
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)