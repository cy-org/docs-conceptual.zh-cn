---
title: "&lt;legacyCorruptedStateExceptionsPolicy&gt; 元素 | Microsoft Docs"
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
  - "<legacyCorruptedStateExceptionsPolicy> 元素"
  - "legacyCorruptedStateExceptionsPolicy 元素"
ms.assetid: e0a55ddc-bfa8-4f3e-ac14-d1fc3330e4bb
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# &lt;legacyCorruptedStateExceptionsPolicy&gt; 元素
指定公共语言运行时是否允许托管代码捕获访问冲突和其他损坏状态异常。  
  
## 语法  
  
```  
<legacyCorruptedStateExceptionsPolicy enabled="true|false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`enabled`|必需的特性。<br /><br /> 指定应用程序将捕获损坏状态异常失败，如访问冲突。|  
  
## enabled 特性  
  
|值|说明|  
|-------|--------|  
|`false`|应用程序将不会捕获损坏状态异常失败，如访问冲突。  这是默认值。|  
|`true`|应用程序将捕获损坏状态异常失败，如访问冲突。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## 备注  
 在 .NET Framework 版本 3.5 和早期版本中，公共语言运行时允许托管代码捕获由损坏进程状态引发的异常。  访问冲突是此类型的异常的一个示例。  
  
 从 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]开始，托管代码不再捕获 `catch` 块中的这些类型的异常。  但您可以通过两种方式重写此更改并保留对损坏状态异常的处理：  
  
-   将 `<legacyCorruptedStateExceptionsPolicy>` 元素的 `enabled` 特性设置为 `true`。  此配置设置在进程范围内适用并会影响所有方法。  
  
 \- 或 \-  
  
-   将 <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute?displayProperty=fullName> 特性应用于包含异常 `catch` 块的方法。  
  
 此配置元素仅在 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 和更高版本中可用。  
  
## 示例  
 下面的示例演示如何指定应用程序应恢复为 [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] 之前的行为，并捕获所有损坏状态异常失败。  
  
```  
<configuration>  
   <runtime>  
      <legacyCorruptedStateExceptionsPolicy enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>   
 [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)