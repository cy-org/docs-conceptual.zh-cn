---
title: "&lt;trace&gt; 的 &lt;listeners&gt; 的 &lt;remove&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<remove> 元素"
  - "remove 元素"
ms.assetid: 9a5cd1b5-be1a-485f-8f0c-2890ad3ef3e0
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# &lt;trace&gt; 的 &lt;listeners&gt; 的 &lt;remove&gt; 元素
从 **Listeners** 集合中移除侦听器。  
  
## 语法  
  
```  
  
<remove name="listener name" />  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|**name**|必需的特性。<br /><br /> 要从 **Listeners** 集合中移除的侦听器的名称。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`listeners`|指定对消息进行收集、存储和路由的侦听器。  侦听器将跟踪输出定向到合适的目标。|  
|`system.diagnostics`|指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。|  
|`trace`|配置 ASP.NET 跟踪服务。|  
  
## 备注  
  
> [!NOTE]
>  从 `Listeners` 集合中移除 <xref:System.Diagnostics.DefaultTraceListener> 将更改 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>、<xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>、<xref:System.Diagnostics.Debug.Fail%2A?displayProperty=fullName> 和 <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=fullName> 方法的行为。  调用 `Assert` 或 `Fail` 方法通常会显示一个消息框，但是如果 <xref:System.Diagnostics.DefaultTraceListener> 不在 `Listeners` 集合中，就不会显示消息框。  
  
## 示例  
 下面的示例说明如何从跟踪 **Listeners** 集合中移除默认的跟踪侦听器。  
  
```  
<configuration>  
   <system.diagnostics>  
      <trace autoflush="true" indentsize="0">  
         <listeners>  
            <remove name="Default" />  
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