---
title: "&lt;assert&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/assert"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#assert"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<assert> 元素"
  - "assert 元素"
ms.assetid: ef4c3229-b151-4d85-8091-e6456af9b935
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# &lt;assert&gt; 元素
指定在调用 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 方法时是否显示消息框；还指定要将消息写入的文件的名称。  
  
## 语法  
  
```  
  
<assert assertuienabled="true|false" logfilename="file name"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`assertuienabled`|可选特性。<br /><br /> 指定当 **Debug.Assert** 方法计算为 **false** 时是否显示消息框。|  
|`logfilename`|可选特性。<br /><br /> 指定当 **Debug.Assert** 计算为 **false** 时要将消息写入的文件的名称。|  
  
## assertuienabled 特性  
  
|值|说明|  
|-------|--------|  
|`true`|显示消息框。  这是默认设置。|  
|`false`|不显示消息框。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定对消息进行收集、存储和路由的跟踪侦听器以及设置跟踪开关的级别。|  
  
## 备注  
 **\<assert\>**元素中的两个特性是可选的。  您可以通过不指定要将消息写入的文件来禁用消息框，或者您可以指定在退出启用的消息框时要将消息写入的文件。  
  
## 示例  
 下面的示例说明如何在调用 **Debug.Assert** 并将消息写入 `c:\log.txt` 时禁用对消息框的显示。  
  
```  
<configuration>  
   <system.diagnostics>  
      <assert assertuienabled="false" logfilename="c:\log.txt"/>  
   </system.diagnostics>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Diagnostics.Debug>   
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)