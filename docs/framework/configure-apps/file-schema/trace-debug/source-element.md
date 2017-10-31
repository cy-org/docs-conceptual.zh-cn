---
title: "&lt;source&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#source"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<source> 元素"
  - "source 元素"
ms.assetid: ecf86505-735d-4844-aaba-266fdd134218
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# &lt;source&gt; 元素
指定启动跟踪消息的跟踪源。  
  
## 语法  
  
```  
<source>   
  <listeners>...</listeners>  
</source>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`name`|可选特性。<br /><br /> 指定跟踪源的名称。|  
|`switchName`|可选特性。<br /><br /> 指定应用程序中的跟踪开关实例的名称。  如果未在某个 `<switches>` 元素中标识该开关，则该值指定开关的级别。|  
|`switchType`|可选特性。<br /><br /> 指定跟踪开关的类型。  如存在，该类型必须是有效的类名，并且不能是空字符串。|  
|`extraAttribute`|可选特性。<br /><br /> 为该跟踪源的 <xref:System.Diagnostics.TraceSource.GetSupportedAttributes%2A> 方法确定的跟踪源特定属性指定该值。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<listeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/listeners-element-for-trace.md)|包含对消息进行收集、存储和路由的侦听器。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。|  
|`sources`|包含启动跟踪消息的跟踪源。|  
  
## 备注  
 此元素可用于计算机配置文件 \(Machine.config\) 和应用程序配置文件。  
  
## 示例  
 下面的示例演示如何使用 `<source>`  元素添加跟踪源 `mySource` 并设置名为 `sourceSwitch` 的源开关的级别。  添加了一个控制台跟踪侦听器，该侦听器将跟踪信息写到控制台。  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="mySource" switchName="sourceSwitch" switchType="System.Diagnostics.SourceSwitch"  >  
        <listeners>  
          <add name="console" type="System.Diagnostics.ConsoleTraceListener" >  
            <filter type="System.Diagnostics.EventTypeFilter" initializeData="Error" />  
          </add>  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
        <switches>  
           <add name="sourceSwitch" value="Warning" />  
        </switches>    
  </system.diagnostics>   
</configuration>  
```  
  
## 请参阅  
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)   
 [Trace Switches](../../../../../docs/framework/debug-trace-profile/trace-switches.md)