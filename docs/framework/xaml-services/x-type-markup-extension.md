---
title: "x:Type Markup Extension | Microsoft Docs"
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
  - "x:TypeExtension"
  - "Type"
  - "x:Type"
  - "xType"
  - "TypeExtension"
helpviewer_keywords: 
  - "x:Type markup extension [XAML Services]"
  - "XAML [XAML Services], x:Type markup extension"
  - "XAML [XAML Services], TargetType attribute"
  - "TargetType attribute [XAML Services]"
  - "Type markup extension in XAML [XAML Services]"
ms.assetid: e0e0ce6f-e873-49c7-8ad7-8b840eb353ec
caps.latest.revision: 27
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 27
---
# x:Type Markup Extension
提供 CLR <xref:System.Type> 对象，该对象是指定的 XAML 类型的基础类型。  
  
## XAML 属性用法  
  
```  
<object property="{x:Type prefix:typeNameValue}" .../>  
```  
  
## XAML 对象元素用法  
  
```  
<x:Type TypeName="prefix:typeNameValue"/>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`prefix`|可选。  映射非默认 XAML 命名空间的前缀。  通常没必要指定前缀。  请参见"备注"。|  
|`typeNameValue`|必选。  可解析为当前默认 XAML 命名空间的类型名；或者所指定的映射前缀（如果提供了 `prefix`）。|  
  
## 备注  
 `x:Type` 对 [!INCLUDE[TLA#tla_cshrp](../../../includes/tlasharptla-cshrp-md.md)] 中的 `typeof()` 运算符或 [!INCLUDE[TLA#tla_visualb](../../../includes/tlasharptla-visualb-md.md)] 中的 `GetType` 运算符都有类似的函数。  
  
 `x:Type` 标记扩展提供采用类型 <xref:System.Type> 的属性的 from\-string 转换行为。  输入为 XAML 类型。  输入 XAML 类型和输出 CLR <xref:System.Type> 之间的关系是：在查找了基于 XAML 架构上下文的必要的 <xref:System.Xaml.XamlType> 和该上下文提供的 <xref:System.Windows.Markup.IXamlTypeResolver> 服务后，输出 <xref:System.Type> 为输入 <xref:System.Xaml.XamlType> 的 <xref:System.Xaml.XamlType.UnderlyingType%2A>。  
  
 在 .NET Framework XAML 服务中，对此标记扩展的处理由 <xref:System.Windows.Markup.TypeExtension> 类定义。  
  
 在特定框架实现中，将 <xref:System.Type> 作为值的一些属性都能直接接受类型的名称（类型的 `Name` 的字符串值）。  但是，实现此类行为是一种复杂的方案。  关于示例，请参见下面的“WPF 用法说明”一节。  
  
 特性语法是最常用于此标记扩展的语法。  在 `x:Type` 标识符字符串之后提供的字符串标记被指定为基础 <xref:System.Windows.Markup.TypeExtension> 扩展类的 <xref:System.Windows.Markup.TypeExtension.TypeName%2A> 值。  在用于 .NET Framework XAML 服务的默认 XAML 架构上下文（基于 CLR 类型）之下，此特性的值为所需类型的 <xref:System.Reflection.MemberInfo.Name%2A>，或包含以用于非默认 XAML 命名空间映射的前缀开头的 <xref:System.Reflection.MemberInfo.Name%2A>。  
  
 `x:Type` 标记扩展可用于对象元素语法。  在这种情况下，指定 <xref:System.Windows.Markup.TypeExtension.TypeName%2A> 属性的值是正确初始化该扩展所必需的。  
  
 `x:Type` 标记扩展，也可以用作一个详细的属性；但是这种用法不是典型的：`<``object` `property``="{x:Type TypeName=``typeNameValue``}" .../>`  
  
## WPF 用法说明  
  
### 默认 XAML 命名空间和类型映射  
 用于 WPF 编程的默认 XAML 命名空间包含大多数典型 XAML 方案需要的 XAML 类型，因此在引用 XAML 类型值时，您通常可以避免前缀。  在以下情况下可能需要映射前缀：所引用的类型来自自定义程序集，或者类型存在于 WPF 程序集内，但位于 CLR 命名空间中，而该命名空间未映射为默认 XAML 命名空间。  有关前缀、XML 命名空间和映射 CLR 命名空间的更多信息，请参见 [WPF XAML 的 XAML 命名空间和命名空间映射](../../../ocs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)。  
  
### 支持作为字符串的类型名的类型属性  
 WPF 支持技术使我们可以指定类型 <xref:System.Type> 的某些属性的值，而无需 `x:Type` 标记扩展用法。  相反，您可以将值指定为命名类型的字符串。  示例包括 <xref:System.Windows.Controls.ControlTemplate.TargetType%2A?displayProperty=fullName> 和 <xref:System.Windows.Style.TargetType%2A?displayProperty=fullName>。  对此行为的支持不是通过类型转换器或标记扩展提供的。  相反，这是通过 <xref:System.Windows.FrameworkElementFactory> 实现的延迟行为。  
  
 Silverlight 支持类似的公约。  事实上，Silverlight 的 XAML 语言中目前不支持 `{x:Type}`，并且不接受在计划支持 WPF\-Silverlight XAML 迁移的一些环境之外使用 `{x:Type}`。  因此，类型名称作为字符串行为是内置在所有 Silverlight 本机性能属性评估中的，其值为 <xref:System.Type>。  
  
## XAML 2009  
 XAML 2009 为泛型类型提供额外的支持，并修改 `x:TypeArguments` 和 `x:Type` 的功能行为以提供此支持。  
  
-   `x:TypeArguments` 和一般对象实例化的相关对象元素可以是除了根之外的元素。  有关更多信息，请参见"XAML 2009" 的[x:TypeArguments Directive](../../../docs/framework/xaml-services/x-typearguments-directive.md)一节。  
  
-   XAML 2009 支持指定标记中泛型类型的限制的语法。  这可以由 `x:TypeArguments`、 `x:Type` 或组合中的两个功能使用。  
  
-   WPF XAML 实现在为负载处理 XAML 2009 时也将此功能为特定框架属性添加到隐式类型转换行为，这些属性使用类型 <xref:System.Type>。  
  
 在 WPF 中，可以使用 XAML 2009 功能，但仅针对松散的 XAML（未进行标记编译的 XAML）。  WPF 的已编译标记的 XAML 以及 XAML 的 BAML 形式当前不支持 XAML 2009 关键字和功能。  
  
## 请参阅  
 <xref:System.Windows.Style>   
 [样式设置和模板化](../../../ocs/framework/wpf/controls/styling-and-templating.md)   
 [XAML 概述 \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [标记扩展和 WPF XAML](../../../ocs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)