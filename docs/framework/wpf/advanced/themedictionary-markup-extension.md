---
title: "ThemeDictionary 标记扩展 | Microsoft Docs"
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
  - "ThemeDictionaryExtension"
  - "ThemeDictionary"
helpviewer_keywords: 
  - "ThemeDictionary 标记扩展"
  - "XAML, ThemeDictionary 标记扩展"
ms.assetid: aa75e10b-13dd-4989-972d-51bab63a05e2
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# ThemeDictionary 标记扩展
为集成第三方控件的自定义控件作者或应用程序提供了一种方法，以加载要在设置控件样式时使用的主题特定的资源字典。  
  
## XAML 属性用法  
  
```  
<object property="{ThemeDictionary assemblyUri}" .../>  
```  
  
## XAML 对象元素用法  
  
```  
<object>  
  <object.property>  
    <ThemeDictionary AssemblyName="assemblyUri"/>  
  <object.property>  
<object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`assemblyUri`|包含主题信息的程序集的[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]。  通查，这是引用较大包中的程序集的 Pack URI。  程序集资源和 Pack URI 可以简化部署问题。  有关更多信息，请参见[WPF 中的 Pack URI](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md)。|  
  
## 备注  
 该扩展旨在仅填充一个特定属性值：<xref:System.Windows.ResourceDictionary.Source%2A?displayProperty=fullName> 的一个值。  
  
 通过使用该扩展，您可以指定一个纯资源程序集，该程序集包含一些仅在向用户系统应用 [!INCLUDE[TLA#tla_aero](../../../../includes/tlasharptla-aero-md.md)] 主题时使用的样式、当 Luna 主题处于活动状态时的其他样式等。  通过使用该扩展，可以自动使控件特定的资源字典的内容无效，并在需要时重新加载这些内容，使其特定于其他主题。  
  
 `assemblyUri` 字符串（<xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A> 属性值）构成了标识哪个字典应用于某个特殊主题的命名约定的基础。  `ThemeDictionary` 的 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A> 逻辑通过生成一个指向某个特殊主题字典变量（包含在预编译的资源程序集中）的[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 来完成该约定。  本文并未将该约定（即主题与一般控件样式设置和页\/应用程序级样式设置之间的交互）作为一个概念进行详细介绍。  使用 `ThemeDictionary` 的基本方案是指定在应用程序级声明的 `ResourceDictionary` 的 <xref:System.Windows.ResourceDictionary.Source%2A> 属性。  将 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 通过 `ThemeDictionary` 扩展而不是作为一个直接的 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 提供给程序集时，扩展程序将提供每当系统主题更改时应用的失效逻辑。  
  
 特性语法是最常用于此标记扩展的语法。  在 `ThemeDictionary` 标识符字符串之后提供的字符串标记被指定为基础 <xref:System.Windows.ThemeDictionaryExtension> 扩展类的 <xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A> 值。  
  
 `ThemeDictionary` 还可以在对象元素语法中使用。  在这种情况下，需要指定 <xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A> 属性的值。  
  
 `ThemeDictionary` 还可以在将 <xref:System.Windows.Markup.StaticExtension.Member%2A> 属性指定为“属性\=值”对的详细特性用法中使用：  
  
```  
<object property="{ThemeDictionary AssemblyName=assemblyUri}" .../>  
```  
  
 如果扩展具有一个以上的可设置属性，或者某些属性是可选的，则详细用法通常会很有用。  由于 `ThemeDictionary` 仅有一个可设置的属性，并且此属性是必需的，因此该详细用法不具有典型性。  
  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器实现中，对此标记扩展的处理由 <xref:System.Windows.ThemeDictionaryExtension> 类定义。  
  
 `ThemeDictionary` 是标记扩展。  当要求转义属性 \(Attribute\) 值应为非文本值或非处理程序名称时，通常会实现标记扩展，相对于只在某些类型或属性 \(Property\) 上放置类型转换器而言，此要求更具有全局性。  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的所有标记扩展在其特性语法中都使用 { 和 } 字符，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器通过这一约定确认标记扩展必须处理该特性。  有关更多信息，请参见 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
## 请参阅  
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [WPF 应用程序资源、内容和数据文件](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md)