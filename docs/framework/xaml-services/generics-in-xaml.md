---
title: "Generics in XAML | Microsoft Docs"
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
  - "generics [XAML Services]"
ms.assetid: 835bfed7-585c-4216-ae67-b674edab8b92
caps.latest.revision: 8
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 8
---
# Generics in XAML
System.Xaml 中实现的 .NET Framework XAML 服务提供对使用泛型 CLR 类型的支持。  此支持包括以类型参数的形式指定泛型约束，以及通过对泛型集合用例调用适当的 `Add` 方法来实施约束。  本主题介绍在 XAML 中使用和引用泛型类型的各个方面。  
  
## x:TypeArguments  
 `x:TypeArguments` 是由 XAML 语言定义的一个指令。  用作受泛型类型支持的 XAML 类型的成员时，`x:TypeArguments` 将泛型的约束类型参数传递给支持构造函数。  有关与 `x:TypeArguments` 的 .NET Framework XAML 服务用法有关的参考语法（包括语法示例），请参见 [x:TypeArguments Directive](../../../docs/framework/xaml-services/x-typearguments-directive.md)。  
  
 由于 `x:TypeArguments` 接受字符串并且具有类型转换器支持，因此通常会在 XAML 用法中声明为特性。  
  
 在 XAML 节点流中，由 `x:TypeArguments` 声明的信息可以从 <xref:System.Xaml.XamlType.TypeArguments%2A?displayProperty=fullName>（位于节点流中的 `StartObject` 位置）获取。  <xref:System.Xaml.XamlType.TypeArguments%2A?displayProperty=fullName> 的返回值是 <xref:System.Xaml.XamlType> 值的列表。  通过调用 <xref:System.Xaml.XamlType.IsGeneric%2A?displayProperty=fullName> 可确定某个 XAML 类型是否表示泛型类型。  
  
## XAML 中用于泛型的规则和语法约定  
 在 XAML 中，必须始终将泛型类型表示为受约束的泛型；不受约束的泛型从不会出现在 XAML 类型系统或 XAML 节点流中，因此无法以 XAML 标记表示。  对于泛型的嵌套类型约束由 `x:TypeArguments` 引用的情况，或对于 `x:Type` 提供对泛型类型的 CLR 类型引用的情况，可以在 XAML 特性语法中引用泛型。  这是通过 .NET Framework XAML 服务定义的 <xref:System.Xaml.Schema.XamlTypeTypeConverter> 类来支持的。  
  
 由 <xref:System.Xaml.Schema.XamlTypeTypeConverter> 启用的 XAML 特性语法形式改变了通常的 MSIL\/CLR 语法约定，该语法约定对泛型的类型和约束使用尖括号，而不是对约束容器使用圆括号。  有关示例，请参见[x:TypeArguments Directive](../../../docs/framework/xaml-services/x-typearguments-directive.md)。  
  
## 泛型和 XAML 2009 功能  
 如果使用 XAML 2009，而不是映射 CLR 基类型以获取常用语言基元的 XAML 类型，则可以使用 [XAML 2009 内置类型](../../../docs/framework/xaml-services/built-in-types-for-common-xaml-language-primitives.md)以作为 `x:TypeArguments` 中的信息项。  例如，可以声明以下内容（不显示前缀映射，但 `x` 是用于 XAML 2009 的 XAML 语言 XAML 命名空间）：  
  
```  
<my:BusinessObject x:TypeArguments="x:String,x:Int32"/>  
```  
  
## WPF 及其他 3.5 版框架中的泛型支持  
 对于专门面向 WPF 的 XAML 2006 用法，还必须对与 `x:TypeArguments` 相同的元素提供 [x:Class](../../../docs/framework/xaml-services/x-class-directive.md)，而且该元素必须是 XAML 文档中的根元素。  根元素必须映射到至少具有一个类型参数的泛型类型。  一个示例是 <xref:System.Windows.Navigation.PageFunction%601>。  
  
 支持泛型用法的可能解决方法包括定义一个可返回泛型类型的自定义标记扩展，或提供一个从泛型类型派生但在它自己的类定义中展平泛型约束的包装类定义。  
  
 在 WPF 中以及面向 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 时，可以将 XAML 2009 功能与 `x:TypeArguments` 一起使用，但仅针对宽松 XAML（未进行标记编译的 XAML）。  WPF 的已编译标记的 XAML 以及 XAML 的 BAML 形式当前不支持 XAML 2009 关键字和功能。  
  
 用于 [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] 的 [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)] 中的自定义工作流不支持泛型 XAML 用法。  
  
## 请参阅  
 [x:TypeArguments Directive](../../../docs/framework/xaml-services/x-typearguments-directive.md)   
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)   
 [Built\-in Types for Common XAML Language Primitives](../../../docs/framework/xaml-services/built-in-types-for-common-xaml-language-primitives.md)