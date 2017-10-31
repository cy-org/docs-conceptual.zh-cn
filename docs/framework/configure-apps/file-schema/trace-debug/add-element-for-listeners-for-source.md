---
title: "&lt;source&gt; 的 &lt;listeners&gt; 的 &lt;add&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<source> 的 <listeners> 的 <add> 元素"
  - "<source> 的 <listeners> 的 add 元素"
  - "initializeData 特性"
ms.assetid: 4ce36ac1-81ef-48e8-b8b2-b5a5b0e2adcb
caps.latest.revision: 15
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 15
---
# &lt;source&gt; 的 &lt;listeners&gt; 的 &lt;add&gt; 元素
将侦听器添加到跟踪源的 `Listeners` 集合。  
  
## 语法  
  
```  
<add name="name"   
  type="TraceListenerClassName, Version, Culture, PublicKeyToken"  
  initializeData="data"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`type`|必需的特性。<br /><br /> 指定侦听器的类型。  必须使用满足[指定完全限定的类型名称](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)中指定的要求的字符串。|  
|`initializeData`|可选特性。<br /><br /> 传递到指定类的构造函数的字符串。  如果该类没有接受字符串的构造函数，则会引发 <xref:System.Configuration.ConfigurationException>。|  
|`name`|可选特性。<br /><br /> 指定侦听器的名称。|  
|`traceOutputOptions`|可选特性。<br /><br /> 指定跟踪源的 <xref:System.Diagnostics.TraceListener.TraceOutputOptions%2A> 属性值。|  
|\[自定义特性\]|可选特性。<br /><br /> 指定由该侦听器的 <xref:System.Diagnostics.TraceListener.GetSupportedAttributes%2A> 方法所标识的特定于侦听器的特性的值。  <xref:System.Diagnostics.DelimitedListTraceListener.Delimiter%2A> 是 <xref:System.Diagnostics.DelimitedListTraceListener> 类所特有的额外特性的示例。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<filter\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-listeners-for-source.md)|向跟踪源的 `Listeners` 集合中的侦听器添加筛选器。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。|  
|`sources`|包含启动跟踪消息的跟踪源。|  
|`source`|指定启动跟踪消息的跟踪源。|  
|`listeners`|指定对消息进行收集、存储和路由的侦听器。|  
  
## 备注  
 随 .NET Framework 一起提供的侦听器类从 <xref:System.Diagnostics.TraceListener> 类派生。  
  
 如果不指定跟踪侦听器的 `name` 特性，则跟踪侦听器的 <xref:System.Diagnostics.TraceListener.Name%2A> 属性会默认为空字符串 \(""\)。  如果应用程序只有一个侦听器，则可以在不指定名称的情况下添加它，还可以通过指定空字符串作为名称来移除它。  但是，如果应用程序有多个侦听器，则应该为每个跟踪侦听器指定唯一名称，这样，便可以在 <xref:System.Diagnostics.TraceSource.Listeners%2A?displayProperty=fullName> 集合中标识和管理各个跟踪侦听器。  
  
> [!NOTE]
>  添加多个相同类型和相同名称的跟踪侦听器将导致仅有一个该类型和名称的侦听器被添加到 `Listeners` 集合中。  但是可以通过编程方式向 `Listeners` 集合添加多个完全相同的侦听器。  
  
 `initializeData` 特性的值取决于您创建的侦听器的类型。  并非所有跟踪侦听器都要求您指定 `initializeData`。  
  
> [!NOTE]
>  当您使用 `initializeData` 特性时，可能会收到编译器警告“未声明‘initializeData’特性”。出现此警告是因为，在根据抽象基类 <xref:System.Diagnostics.TraceListener> 验证配置设置时，该基类不能识别 `initializeData` 特性。  通常，如果跟踪侦听器实现具有带参数的构造函数，则可以忽略此警告。  
  
 下表说明 .NET Framework 中包含的跟踪侦听器，同时描述了这些侦听器的 `initializeData` 特性值。  
  
|跟踪侦听器类|initializeData 特性值|  
|------------|------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=fullName>|<xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A> 构造函数的 `useErrorStream` 值。将 `initializeData` 特性设置为“`true`”可将跟踪和调试输出写入标准错误流；将它设置为“`false`”可写入标准输出流。|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=fullName>|<xref:System.Diagnostics.DelimitedListTraceListener> 写入的文件名。|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName>|现有的事件日志源的名称。|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=fullName>|<xref:System.Diagnostics.EventSchemaTraceListener> 写入的文件的名称。|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=fullName>|<xref:System.Diagnostics.TextWriterTraceListener> 写入的文件的名称。|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=fullName>|<xref:System.Diagnostics.XmlWriterTraceListener> 写入的文件的名称。|  
  
## 配置文件  
 此元素可用于计算机配置文件 \(Machine.config\) 和应用程序配置文件。  
  
## 示例  
 下面的示例演示如何使用 `<add>` 元素将侦听器 `console` 和 `textListener` 添加到跟踪源 `TraceSourceApp` 的 `Listeners` 集合中。  `textListener` 侦听器将跟踪输出写入文件 myListener.log。  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="TraceSourceApp" switchName="sourceSwitch"   
        switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console"   
            type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="textListener"/>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"   
        type="System.Diagnostics.TextWriterTraceListener"   
        initializeData="myListener.log"/>  
    </sharedListeners>  
    <switches>  
      <add name="sourceSwitch" value="Warning"/>  
    </switches>  
  </system.diagnostics>  
</configuration>   
```  
  
## 请参阅  
 <xref:System.Diagnostics.TraceSource>   
 <xref:System.Diagnostics.TraceListener>   
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)   
 [Trace Listeners](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)