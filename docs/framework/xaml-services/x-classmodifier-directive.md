---
title: "x:ClassModifier Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "xClassModifier"
  - "x:ClassModifier"
  - "ClassModifier"
helpviewer_keywords: 
  - "XAML [XAML Services], x:ClassModifier attribute"
  - "x:ClassModifier attribute [XAML Services]"
  - "ClassModifier attribute in XAML [XAML Services]"
ms.assetid: ef30ab78-d334-4668-917d-c9f66c3b6aea
caps.latest.revision: 22
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 21
---
# x:ClassModifier Directive
在同时提供了 `x:Class` 的情况下，修改 XAML 编译行为。  具体而言，不必创建有 `Public` 访问级别（默认值）的 `class` 分部类，提供的 `x:Class` 是以 `NotPublic` 的访问级别创建的。  此行为会影响生成的程序集中的类的访问级别。  
  
## XAML 属性用法  
  
```  
<object x:Class="namespace.classname" x:ClassModifier="NotPublic">  
   ...  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|*NotPublic*|根据您所使用的代码隐藏编程语言，所传递的用于指定 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 与 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 的确切字符串会有所不同。  请参见"备注"。|  
  
## 依赖项  
 还必须对同一元素提供 [x:Class](../../../docs/framework/xaml-services/x-class-directive.md)，并且该元素必须是页中的根元素。  有关更多信息，请参见 [\[MS\-XAML\] Section 4.3.1.8](http://go.microsoft.com/fwlink/?LinkId=114525)。  
  
## 备注  
 .NET 框架 XAML 服务使用中 `x:ClassModifier` 的值中随不同的编程语言而不同。  要使用的字符串取决于每种语言如何实现其 <xref:System.CodeDom.Compiler.CodeDomProvider> 和其返回的用来定义 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 和 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 意义的类型转换器，以及该语言是否区分大小写。  
  
-   对于 [!INCLUDE[TLA2#tla_cshrp](../../../includes/tla2sharptla-cshrp-md.md)]，所传递的用于指定 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 的字符串是 `internal`。  
  
-   对于 [!INCLUDE[TLA2#tla_visualbnet](../../../includes/tla2sharptla-visualbnet-md.md)]，为指定 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 而传递的字符串是 `Friend`。  
  
-   对于 [!INCLUDE[TLA2#tla_cppcli](../../../includes/tla2sharptla-cppcli-md.md)]，不存在支持编译 XAML 的目标文件；因此未指定要传递的值。  
  
 还可以指定 <xref:System.Reflection.TypeAttributes?displayProperty=fullName>（[!INCLUDE[TLA2#tla_cshrp](../../../includes/tla2sharptla-cshrp-md.md)] 中为 `public`，[!INCLUDE[TLA2#tla_visualb](../../../includes/tla2sharptla-visualb-md.md)] 中为 `Public`）；但是，指定 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 并不常见，因为 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 已是默认行为。  
  
 其他具有同等用户代码访问级别限制的值（例如 [!INCLUDE[TLA2#tla_cshrp](../../../includes/tla2sharptla-cshrp-md.md)] 中的 `private`）与 `x:ClassModifier` 不相关，因为 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 不支持嵌套类引用，因此， 修饰符具有同样的效果。  
  
## 安全说明  
 `x:ClassModifier` 中声明的访问级别仍将取决于特定框架的解释及其功能。  如果该类是通过包 URI 引用从 WPF 资源进行引用的，当 `x:ClassModifier` 为 `internal` 时，WPF 将包括加载和实例化类型的功能。  这种情况或由其他框架实现的潜在其他类似情况的后果是，不完全依赖 `x:ClassModifier` 来阻止所有可能的实例化尝试。  
  
## 请参阅  
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)   
 [WPF 中的代码隐藏和 XAML](../../../ocs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)   
 [x:FieldModifier Directive](../../../docs/framework/xaml-services/x-fieldmodifier-directive.md)   
 [安全性 \(WPF\)](../../../ocs/framework/wpf/security-wpf.md)   
 [Types Migrated from WPF to System.Xaml](../../../docs/framework/xaml-services/types-migrated-from-wpf-to-system-xaml.md)