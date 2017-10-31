---
title: "&lt;supportPortability&gt; 元素 | Microsoft Docs"
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
  - "<supportPortability> 元素"
  - "supportPortability 元素"
ms.assetid: 6453ef66-19b4-41f3-b712-52d0c2abc9ca
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# &lt;supportPortability&gt; 元素
指定应用程序可以在 .NET Framework 的两个不同实现中引用同一个程序集，方法为禁用默认行为，该默认行为因应用程序优先级目的将程序集处理为等同物。  
  
## 语法  
  
```  
<supportPortability PKT="public_key_token" enabled="true|false"/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|PKT|必需的特性。<br /><br /> 指定受影响程序集的公钥标记，形式为字符串。|  
|enabled|可选特性。<br /><br /> 指定是否应启用指定的 .NET Framework 实现之间的可移植性的支持。|  
  
## enabled 特性  
  
|值|描述|  
|-------|--------|  
|true|启用对指定的 .NET Framework 程序集实现之间的可移植性的支持。  这是默认值。|  
|false|禁用对指定的 .NET Framework 程序集实现之间的可移植性的支持。  这使应用程序具有指定的程序集的多个实现的引用。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
|`assemblyBinding`|包含有关程序集版本重定向和程序集位置的信息。|  
  
## 备注  
 从 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 开始，将自动为应用程序提供支持，使其可以使用两个 .NET Framework 实现之一，如 .NET Framework 实现或 .NET Framework for Silverlight 实现。  特定的 .NET Framework 的两个实现都由程序集联编程序视为等同。  在几个方案中，此应用程序的可移植性功能会产生问题。  在这些方案中 `<supportPortability>` 元素可用于禁用此功能。  
  
 其中一种方案是必须同时引用特定引用程序集的 .NET Framework 版本和 .NET Framework for Silverlight 版本。  例如，以 Windows Presentation Foundation \(WPF\) 编写的 XAML 设计器可能需要同时引用设计器用户界面的 WPF 桌面实现以及 Silverlight 实现中附带的 WPF 子集。  默认情况下，单独引用会导致编译器错误，因为程序集绑定将这两个程序集视为等效。  此元素禁用默认行为，并允许编译成功。  
  
> [!IMPORTANT]
>  为了让编译器将信息传递给公共语言运行库的程序集绑定逻辑，必须使用 `/appconfig` 编译器选项来指定包含此元素的 app.config 文件的位置。  
  
## 示例  
 下面的示例使应用程序可以具有对任何 .NET Framework 程序集的 .NET Framework 实现和 .NET Framework for Silverlight 实现的引用，该程序集存在于两个实现中。  `/appconfig` 编译器选项必须用于指定此 app.config 文件的位置。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding>  
         <supportPortability PKT="7cec85d7bea7798e" enable="false"/>  
         <supportPortability PKT="31bf3856ad364e35" enable="false"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## 请参阅  
 [\/appconfig（C\# 编译器选项）](http://msdn.microsoft.com/library/ee523958.aspx)   
 [.NET Framework Assembly Unification Overview](http://msdn.microsoft.com/zh-cn/8d8cc65e-031d-463b-bde3-2c6dc2e3bc48)