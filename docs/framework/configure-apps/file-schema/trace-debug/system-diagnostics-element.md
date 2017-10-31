---
title: "&lt;system.diagnostics&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#system.diagnostics"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<system.diagnostics> 元素"
  - "system.diagnostics 元素"
ms.assetid: 3f348f42-fa72-4ff2-aa1c-bb9eecad4bb2
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 15
---
# &lt;system.diagnostics&gt; 元素
指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。  
  
## 语法  
  
```  
<system.diagnostics>   
</system.diagnostics>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<assert\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/assert-element.md)|指定在调用 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 方法时是否显示消息框；还指定要将消息写入的文件的名称。|  
|[\<performanceCounters\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/performancecounters-element.md)|指定由性能计数器共享的全局内存的大小。|  
|[\<sharedListeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sharedlisteners-element.md)|包含任何源或跟踪元素都能引用的侦听器。  标识为共享侦听器的侦听器可按名称添加到源或跟踪。|  
|[\<sources\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sources-element.md)|指定启动跟踪消息的跟踪源。|  
|[\<switches\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/switches-element.md)|包含跟踪开关以及设置跟踪开关的级别。|  
|[\<trace\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/trace-element.md)|包含对跟踪消息进行收集、存储和路由的侦听器。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
  
## 示例  
 下面的例子演示了如何将一个查找开关和查找侦听器嵌入到**\<system.diagnostics\>**元素。  `General` 跟踪开关被设置为 [TraceLevel.Error](frlrfSystemDiagnosticsTraceLevelClassTopic) 级别。  跟踪侦听器 `myListener` 创建名为 `MyListener.log` 的文件并将输出写入该文件。  
  
> [!NOTE]
>  在 .NET Framework 2.0 版中，可以使用文本为开关指定值。  例如，您可以为 <xref:System.Diagnostics.BooleanSwitch> 指定 `true`，或将表示枚举值的文本，（如 `Error`）用于 <xref:System.Diagnostics.TraceSwitch>。  `<add name="myTraceSwitch" value="Error" />` 行与 `<add name="myTraceSwitch" value="1" />` 等效。  
  
```  
<configuration>  
   <system.diagnostics>  
      <switches>  
         <add name="General" value="4" />  
      </switches>  
      <trace autoflush="true" indentsize="2">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, System, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="MyListener.log" traceOutputOptions="ProcessId, LogicalOperationStack, Timestamp, ThreadId, Callstack, DateTime" />  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Diagnostics.Trace>   
 <xref:System.Diagnostics.Debug>   
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)