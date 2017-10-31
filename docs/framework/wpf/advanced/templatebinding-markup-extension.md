---
title: "TemplateBinding 标记扩展 | Microsoft Docs"
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
  - "TemplateBinding"
  - "TemplateBindingExtension"
helpviewer_keywords: 
  - "TemplateBinding 标记扩展"
  - "XAML, TemplateBinding 标记扩展"
ms.assetid: 1d25bbfc-dbc2-499d-9f12-419d23d4ac6a
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# TemplateBinding 标记扩展
连接某一控件模板中的属性值，使之成为模板化控件上另一个属性的值。  
  
## XAML 属性用法  
  
```  
<object property="{TemplateBinding sourceProperty}" .../>  
```  
  
## XAML 特性用法（适用于模板或样式的 Setter 属性）  
  
```  
<Setter Property="propertyName" Value="{TemplateBinding sourceProperty}" .../>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`propertyName`|在资源库语法中设置的属性的 <xref:System.Windows.DependencyProperty.Name%2A?displayProperty=fullName>。|  
|`sourceProperty`|另一个在要模板化的类型上存在的依赖项属性，由其 <xref:System.Windows.DependencyProperty.Name%2A?displayProperty=fullName> 来指定。<br /><br /> \- 或 \-<br /><br /> 由要模板化的目标类型之外的类型所定义的“dotted\-down”属性名称。  这实际上是 <xref:System.Windows.PropertyPath>。  请参阅[PropertyPath XAML 语法](../../../../docs/framework/wpf/advanced/propertypath-xaml-syntax.md)。|  
  
## 备注  
 对于模板方案来说，`TemplateBinding` 是[绑定](../../../../docs/framework/wpf/advanced/binding-markup-extension.md)的优化形式，类似于使用 `{Binding RelativeSource={RelativeSource TemplatedParent}}` 构造的 `Binding`。  `TemplateBinding` 始终为单向绑定，即使所涉及的属性默认为双向绑定。  所涉及的两个属性都必须是依赖项属性。  
  
 [RelativeSource](../../../../docs/framework/wpf/advanced/relativesource-markupextension.md) 是另一个标记扩展，有时与 `TemplateBinding` 结合使用或者代替它使用，以便在模板中执行相对属性绑定。  
  
 此处未介绍控件模板概念；有关详细信息，请参阅 [Control 样式和模板](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)。  
  
 特性语法是最常用于该标记扩展的语法。  在 `TemplateBinding` 标识符字符串之后提供的字符串标记被指定为基础 <xref:System.Windows.TemplateBindingExtension> 扩展类的 <xref:System.Windows.TemplateBindingExtension.Property%2A> 值。  
  
 对象元素语法也可行，但因为没有实际的应用，所以未进行演示。  `TemplateBinding` 用于使用计算的表达式来填充资源库内的值，因此使用 `TemplateBinding` 的对象元素语法来填充 `<Setter.Property>` 属性元素语法就会变得繁冗而多余。  
  
 `TemplateBinding` 还可以在详细特性用法中使用，以便将 <xref:System.Windows.TemplateBindingExtension.Property%2A> 属性指定为一个 property\=value 对：  
  
```  
<object property="{TemplateBinding Property=sourceProperty}" .../>  
```  
  
 如果扩展具有一个以上的可设置属性，或者某些属性是可选的，则详细用法通常会很有用。  由于 `TemplateBinding` 仅有一个可设置的属性，并且此属性是必需的，因此该详细用法不具有典型性。  
  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] XAML 处理器实现中，对此标记扩展的处理由 <xref:System.Windows.TemplateBindingExtension> 类来定义。  
  
 `TemplateBinding` 是标记扩展。  当要求转义特性值应为非文本值或非处理程序名称时，通常会实现标记扩展，相对于只在某些类型或属性上放置类型转换器而言，此要求更具有全局性。  XAML 中的所有标记扩展在其特性语法中均使用 `{` 和 `}` 字符，正是依据这一约定，XAML 处理器认定标记扩展必须处理特性。  有关详细信息，请参阅[标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
## 请参阅  
 <xref:System.Windows.Style>   
 <xref:System.Windows.Controls.ControlTemplate>   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [RelativeSource MarkupExtension](../../../../docs/framework/wpf/advanced/relativesource-markupextension.md)   
 [绑定标记扩展](../../../../docs/framework/wpf/advanced/binding-markup-extension.md)