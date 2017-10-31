---
title: "StaticResource 标记扩展 | Microsoft Docs"
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
  - "StaticResource"
  - "StaticResourceExtension"
helpviewer_keywords: 
  - "StaticResource 标记扩展"
  - "XAML, StaticResource 标记扩展"
ms.assetid: 97af044c-71f1-4617-9a94-9064b68185d2
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# StaticResource 标记扩展
通过查找对已定义资源的引用，为任何 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 属性特性提供值。  对该资源的查找行为类似于加载时查找，它会查找以前从当前 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页的标记中加载的资源以及其他应用程序源，并且将该资源值生成为运行时对象中的属性值。  
  
## XAML 属性用法  
  
```  
<object property="{StaticResource key}" .../>  
```  
  
## XAML 对象元素用法  
  
```  
<object>  
  <object.property>  
<StaticResource ResourceKey="key" .../>  
  </object.property>  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`key`|所请求的资源的键。  如果资源是在标记中创建的，则这个键最初是由 [x:Key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)分配的；如果资源是在代码中创建的，则这个键是在调用 <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=fullName> 时作为 `key` 参数提供的。|  
  
## 备注  
  
> [!IMPORTANT]
>  `StaticResource` 不得尝试对 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件中按词法进一步定义的资源进行前向引用。  不支持这种尝试。即使这种前向引用没有失败，当搜索表示 <xref:System.Windows.ResourceDictionary> 的内部哈希表时，尝试前向引用也会导致加载时性能下降。  为了获得最佳效果，应调整资源字典的撰写方式，从而避免前向引用。  如果不能避免前向引用，请改用 [DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)。  
  
 指定的 <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> 应与某个现有资源对应，此现有资源使用页、应用程序、可用控件主题和外部资源或系统资源中某一级别的 [x:Key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)来标识。  资源查找按照该顺序执行。  有关静态资源和动态资源的资源查找行为的更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
 资源键可以是通过 [XamlName 语法](../../../../docs/framework/xaml-services/xamlname-grammar.md)定义的任何字符串。  资源键也可以是其他对象类型，如 <xref:System.Type>。  <xref:System.Type> 键是通过隐式样式键按主题设置控件样式的基础。  有关更多信息，请参见[控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)。  
  
 引用资源的其他声明方式是 [DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)。  
  
 特性语法是最常用于此标记扩展的语法。  在 `StaticResource` 标识符字符串之后提供的字符串标记被分配为基础 <xref:System.Windows.StaticResourceExtension> 扩展类的 <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> 值。  
  
 `StaticResource` 可以在对象元素语法中使用。  在这种情况下，需要指定 <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> 属性的值。  
  
 `StaticResource` 还可以在将 <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> 属性指定为“属性\=值”对的详细特性用法中使用：  
  
```  
<object property="{StaticResource ResourceKey=key}" .../>  
```  
  
 如果扩展具有一个以上的可设置属性，或者某些属性是可选的，则详细用法通常会很有用。  由于 `StaticResource` 仅有一个可设置的属性，并且此属性是必需的，因此该详细用法不具有典型性。  
  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器实现中，对此标记扩展的处理由 <xref:System.Windows.StaticResourceExtension> 类定义。  
  
 `StaticResource` 是标记扩展。  当要求转义属性 \(Attribute\) 值应为非文本值或非处理程序名称时，通常会实现标记扩展，相对于只在某些类型或属性 \(Property\) 上放置类型转换器而言，此要求更具有全局性。  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的所有标记扩展在其特性语法中都使用 { 和 } 字符，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器通过这一约定确认标记扩展必须处理该特性。  有关更多信息，请参见 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
## 请参阅  
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [资源和代码](../../../../docs/framework/wpf/advanced/resources-and-code.md)