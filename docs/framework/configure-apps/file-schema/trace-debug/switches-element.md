---
title: "&lt;switches&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/switches"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#switches"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<switches> 元素"
  - "switches 元素"
  - "跟踪开关, <switches> 元素"
ms.assetid: 4cf36786-b89a-40e2-a0f1-86bb9b783343
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# &lt;switches&gt; 元素
包含跟踪开关以及设置跟踪开关的级别。  
  
## 语法  
  
```  
  
      <switches>   
</switches>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<添加\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/add-element-for-switches.md)|指定设置跟踪开关的级别。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`System.diagnostics`|指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。|  
  
## 备注  
 可以通过将跟踪开关的级别放置到配置文件中来更改该级别。  如果该开关是 <xref:System.Diagnostics.BooleanSwitch>，则可以将其打开和关闭。  如果该开关是 <xref:System.Diagnostics.TraceSwitch>，则可为其分配不同的级别，以指定跟踪类型或应用程序输出的调试消息。  
  
## 示例  
 下面的示例演示了如何使用**\<switch\>**元素设置`General`查找开关为[TraceLevel.Error](frlrfSystemDiagnosticsTraceLevelClassTopic)级，并且启用`Data`布尔型查找开关。  
  
```  
<configuration>  
   <system.diagnostics>  
      <switches>  
         <add name="General" value="4" />  
         <add name="Data" value="1" />  
      </switches>  
   </system.diagnostics>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Diagnostics.Switch>   
 <xref:System.Diagnostics.TraceSwitch>   
 <xref:System.Diagnostics.BooleanSwitch>   
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)