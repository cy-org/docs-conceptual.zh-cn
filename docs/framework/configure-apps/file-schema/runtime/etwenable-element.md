---
title: "&lt;etwEnable&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<etwEnable> 元素"
  - "etwEnable 元素"
ms.assetid: 29dde982-6d8b-4099-8867-ad0d7733f6dc
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# &lt;etwEnable&gt; 元素
指定是否为公共语言运行时事件启用 Windows 事件跟踪 \(ETW\)。  
  
## 语法  
  
```  
<etwEnable enabled="true|false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|enabled|必需的特性。<br /><br /> 指定是否应启用 ETW。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|true|启用 ETW。  这是从 Windows 的 Windows Vista 和 Windows Server 2008 操作系统开始的默认设置。|  
|false|禁用 ETW。  这是 Windows 的早期版本的默认设置。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 从 Windows Vista 开始，默认情况下启用 ETW。  使用此元素为应用程序禁用 ETW。  在早期的 Windows 版本中，使用此元素来启用应用程序的 ETW。  
  
> [!NOTE]
>  可以通过使用注册表设置在服务器上全局启用或禁用 ETW。  请参见 [控制 .NET Framework 日志记录](../../../../../docs/framework/performance/controlling-logging.md)。  
  
## 示例  
 下面的示例演示如何为某个应用程序启用 ETW 跟踪。  
  
```  
<configuration>  
   <runtime>  
      <etwEnable enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [控制 .NET Framework 日志记录](../../../../../docs/framework/performance/controlling-logging.md)