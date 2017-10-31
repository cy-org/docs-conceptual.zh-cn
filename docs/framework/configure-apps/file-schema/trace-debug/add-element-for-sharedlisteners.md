---
title: "&lt;sharedListeners&gt; 的 &lt;add&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners/add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<sharedListeners> 的 <add> 元素"
  - "<sharedListeners> 的 add 元素"
  - "initializeData 特性"
ms.assetid: 1595e1bc-2492-421f-8384-7f382eb8eb57
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# &lt;sharedListeners&gt; 的 &lt;add&gt; 元素
将侦听器添加到 `sharedListeners` 集合中。  `sharedListeners` 是任何 [\<source\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/source-element.md) 或 [\<trace\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/trace-element.md) 可以引用的侦听器的集合。默认情况下，`sharedListeners` 集合中的侦听器未放在 `Listeners` 集合中。  必须将它们按名称添加到 [\<source\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/source-element.md) 或 [\<trace\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/trace-element.md)。  不能在运行时在代码中获取 `sharedListeners` 集合中的侦听器。  
  
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
|`name`|必需的特性。<br /><br /> 指定用于将共享侦听器添加到 `Listeners` 集合的侦听器的名称。|  
|`type`|必需的特性。<br /><br /> 指定侦听器的类型。  必须使用满足[指定完全限定的类型名称](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)中指定的要求的字符串。|  
|`initializeData`|可选特性。<br /><br /> 传递到指定类的构造函数的字符串。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<filter\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-sharedlisteners.md)|向 `sharedListeners` 集合中的侦听器添加筛选器。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。|  
|`sharedListeners`|任何源或跟踪元素都能引用的侦听器的集合。|  
  
## 备注  
 随 .NET Framework 一起提供的侦听器类从 <xref:System.Diagnostics.TraceListener> 类派生。  `name` 特性的值用于将共享侦听器添加到跟踪或跟踪源的 `Listeners` 集合。  `initializeData` 特性的值取决于您创建的侦听器的类型。  并非所有跟踪侦听器都要求您指定 `initializeData`。  
  
> [!NOTE]
>  当您使用 `initializeData` 特性时，可能会收到编译器警告“未声明‘initializeData’特性”。出现此警告是因为，在根据抽象基类 <xref:System.Diagnostics.TraceListener> 验证配置设置时，该基类不能识别 `initializeData` 特性。  通常，如果跟踪侦听器实现具有带参数的构造函数，则可以忽略此警告。  
  
 下表说明 .NET Framework 中包含的跟踪侦听器，同时描述了这些侦听器的 `initializeData` 特性值。  
  
|跟踪侦听器类|initializeData 特性值|  
|------------|------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener>|<xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A> 构造函数的 `useErrorStream` 值。将 `initializeData` 特性设置为“`true`”可将跟踪和调试输出写入标准错误流；将它设置为“`false`”可写入标准输出流。|  
|<xref:System.Diagnostics.DelimitedListTraceListener>|<xref:System.Diagnostics.DelimitedListTraceListener> 写入的文件名。|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName>|现有的事件日志源的名称。|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=fullName>|<xref:System.Diagnostics.EventSchemaTraceListener> 写入的文件的名称。|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=fullName>|<xref:System.Diagnostics.TextWriterTraceListener> 写入的文件的名称。|  
|<xref:System.Diagnostics.XmlWriterTraceListener>|<xref:System.Diagnostics.XmlWriterTraceListener> 写入的文件的名称。|  
  
## 配置文件  
 此元素可用于计算机配置文件 \(Machine.config\) 和应用程序配置文件。  
  
## 示例  
 如下的例子演示了如何使用`<add>`元素来增加 <xref:System.Diagnostics.TextWriterTraceListener> `textListener`到`sharedListeners` 集合。`textListener`按名字被增加到查找资源`TraceSourceApp`的`Listeners`集合。  `textListener` 侦听器将跟踪输出写入文件 myListener.log。  
  
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