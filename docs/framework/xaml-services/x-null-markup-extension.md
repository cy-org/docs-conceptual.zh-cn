---
title: "x:Null Markup Extension | Microsoft Docs"
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
  - "NullExtension"
  - "x:NullExtension"
  - "x:Null"
  - "Null"
  - "xNull"
helpviewer_keywords: 
  - "Null markup extension in XAML [XAML Services]"
  - "x:Null markup extension [XAML Services]"
  - "XAML [XAML Services], x:Null markup extension"
ms.assetid: 2e3ccc21-4996-481d-91b5-3910d8b3bfa3
caps.latest.revision: 20
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 20
---
# x:Null Markup Extension
将 `null` 指定为 XAML 成员的值。  
  
## XAML 属性用法  
  
```  
<object property="{x:Null}" .../>  
```  
  
## 备注  
 在 [!INCLUDE[TLA#tla_cshrp](../../../includes/tlasharptla-cshrp-md.md)] 和 [!INCLUDE[TLA#tla_cpp](../../../includes/tlasharptla-cpp-md.md)] 中，null 引用的关键字是 null。  null 引用的 [!INCLUDE[TLA#tla_visualb](../../../includes/tlasharptla-visualb-md.md)] 关键词为 `Nothing`，但您应始终使用 `{x:Null}` 作为 XAML 用法，无论是哪一种代码隐藏语言与 XAML 关联。  
  
 `x:Null` 标记扩展没有可设置的属性。  
  
 null 用法通常与 CLR <xref:System.Nullable%601> 值的 XAML 成员公开相关。  
  
 `x:Null` 标记扩展（如所有 XAML 标记扩展）使用括号 \(`{,}`\) 将对特性值的处理转义为非文字或事件处理程序引用。  特性语法是最常用于此标记扩展的语法。  对象元素语法 `\<x:Null />` 从技术上讲是可行的，但是极少使用，因为 `x:Null` 标记扩展没有位置参数，也没有构造参数。  
  
 有关标记扩展的信息，请参见[标记扩展和 WPF XAML](../../../ocs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
 在 .NET Framework XAML 服务中，对此标记扩展的处理由 <xref:System.Windows.Markup.NullExtension> 类定义。  
  
## WPF 用法说明  
 请注意，`null` 不一定是引用类型依赖项属性的初始未设置值。  初始默认值因每个依赖属性而异，可以基于特定于属性的元数据。  许多依赖项属性由于它们的验证回调实现而不接受 `null` 值，不管是通过标记还是代码。  有关依赖项属性的更多信息，请参见[依赖项属性概述](../../../ocs/framework/wpf/advanced/dependency-properties-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.DependencyProperty.UnsetValue>   
 [XAML 概述 \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [标记扩展和 WPF XAML](../../../ocs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)