---
title: "x:FieldModifier Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FieldModifier attribute in XAML [XAML Services]"
  - "x:FieldModifier attribute [XAML Services]"
  - "XAML [XAML Services], x:FieldModifier attribute"
ms.assetid: ed427cd4-2f35-4d24-bd2f-0fa7b71ec248
caps.latest.revision: 15
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 14
---
# x:FieldModifier Directive
修改 XAML 编译行为，使用 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 访问方式来定义命名对象引用的字段，而不使用 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 默认行为。  
  
## XAML 属性用法  
  
```  
<object x:FieldModifier="Public".../>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|*Public*|根据所使用的代码隐藏编程语言，您传递的用于指定 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 与 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 的确切字符串会有所不同。  请参见"备注"。|  
  
## 依赖项  
 如果 XAML 生产在任意位置使用 `x:FieldModifier`，则该 XAML 生产的根元素必须声明 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)。  
  
## 备注  
 声明类或其成员的常规访问级别时，不需要使用 `x:FieldModifier`。  只有在处理特定 XAML 对象（该对象是 XAML 生产的一部分）时，它才与 XAML 处理行为相关，并成为应用程序对象图中可以访问的对象。  默认情况下，此类对象的字段引用保持为私有，这样可防止控件使用方直接修改对象图。  相反，控件使用者应使用由编程模型启用的标准模式（如获取布局根、子元素集合、专用公共属性等）来修改对象图。  
  
 `x:FieldModifier` 特性的值因编程语言而异，且其目的可因特定框架而异。  要使用的字符串取决于每种语言如何实现其 <xref:System.CodeDom.Compiler.CodeDomProvider> 和其返回的用来定义 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 和 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 意义的类型转换器，以及该语言是否区分大小写。  
  
-   对于 [!INCLUDE[TLA2#tla_cshrp](../../../includes/tla2sharptla-cshrp-md.md)]，所传递的用于指定 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 的字符串是 `public`。  
  
-   对于 [!INCLUDE[TLA2#tla_visualbnet](../../../includes/tla2sharptla-visualbnet-md.md)]，所传递的用于指定 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 的字符串是 `Public`。  
  
-   对于 [!INCLUDE[TLA2#tla_cppcli](../../../includes/tla2sharptla-cppcli-md.md)]，XAML 的目标当前不存在；因此未定义要传递的字符串。  
  
 也可以指定 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> \(`internal` 中的 [!INCLUDE[TLA2#tla_cshrp](../../../includes/tla2sharptla-cshrp-md.md)], `Friend` 中的 [!INCLUDE[TLA2#tla_visualb](../../../includes/tla2sharptla-visualb-md.md)]\) 但指定 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 但这不常见，因为 `NotPublic` 已是默认行为。  
  
 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> 是默认行为，其原因是程序集的外部代码编译的 XAML 需要访问 XAML 创建的元素并不常见。  WPF 安全体系结构与 XAML 编译行为相结合，除非特意设置 `x:FieldModifier`，否则不会将存储元素实例的字段声明为公共字段。  
  
 `x:FieldModifier` 仅与具有 [x:Name Directive](../../../docs/framework/xaml-services/x-name-directive.md)的元素相关，因为该字段成为公共字段之后，该名称将用于引用该字段。  
  
 默认情况下，根元素的分部类是公共的；但可以使用 [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md)使其成为非公共类。  [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md)也影响根元素类的实例的访问级别。  可以在根元素上同时放置 `x:Name` 和 `x:FieldModifier`，但这仅会使公共字段成为根元素的副本，真正的根元素类访问级别仍受 [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md)控制。  
  
## 请参阅  
 [XAML 及 WPF 的自定义类](../../../ocs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)   
 [WPF 中的代码隐藏和 XAML](../../../ocs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)   
 [x:Name Directive](../../../docs/framework/xaml-services/x-name-directive.md)   
 [生成 WPF 应用程序 \(WPF\)](../../../ocs/framework/wpf/app-development/building-a-wpf-application-wpf.md)   
 [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md)