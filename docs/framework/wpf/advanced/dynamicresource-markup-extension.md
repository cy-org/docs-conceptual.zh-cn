---
title: "DynamicResource 标记扩展 | Microsoft Docs"
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
  - "DynamicResource"
  - "DynamicResourceExtension"
helpviewer_keywords: 
  - "DynamicResource 标记扩展"
  - "XAML, DynamicResource 标记扩展"
ms.assetid: 7324f243-03af-4c2b-b0db-26ac6cdfcbe4
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# DynamicResource 标记扩展
为任何 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 属性特性提供值，该值将推迟为对已定义的资源的引用。  该资源的查找行为与运行时查找类似。  
  
## XAML 属性用法  
  
```  
<object property="{DynamicResource key}" .../>  
```  
  
## XAML 属性元素用法  
  
```  
<object>  
  <object.property>  
    <DynamicResource ResourceKey="key" .../>  
  </object.property>  
</object>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`key`|所请求的资源的键。  如果资源是在标记中创建的，则这个键最初是由 [x:Key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)分配的；如果资源是在代码中创建的，则这个键是在调用 <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=fullName> 时作为 `key` 参数提供的。|  
  
## 备注  
 `DynamicResource` 将在初始编译过程中创建一个临时表达式，因而会将资源查找延迟到实际需要所请求的资源值来构造对象时才执行。  这可能是在加载 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页之后。  将基于键搜索在所有活动的资源字典中查找资源值（从当前页范围开始），并且资源值将取代编译期间的占位符表达式。  
  
> [!IMPORTANT]
>  从依赖项属性的优先级的角度而言，`DynamicResource` 表达式与应用动态资源引用的位置等效。  如果为先前已具有一个 `DynamicResource` 表达式作为本地值的属性设置本地值，则会完全移除 `DynamicResource`。  有关详细信息，请参见[依赖项属性值优先级](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md)。  
  
 相对于 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)而言，某些资源访问方案对于 `DynamicResource` 尤其适合。  有关 `DynamicResource` 和 `StaticResource` 各自所具有的优势和性能影响的讨论，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
 指定的 <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> 应当对应于页面、应用程序、可用控件主题和外部资源或者系统资源中某一级别的 [x:Key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)所确定的现有资源，并且资源查找也将按此顺序进行。  有关静态资源和动态资源的资源查找的更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
 资源键可以是通过 [XamlName 语法](../../../../docs/framework/xaml-services/xamlname-grammar.md)定义的任何字符串。  资源键也可以是其他对象类型，如 <xref:System.Type>。  <xref:System.Type> 键是按主题设置控件样式的基础。  有关更多信息，请参见[控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)。  
  
 用于查找资源值的 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]（如 <xref:System.Windows.FrameworkElement.FindResource%2A>）采用与 `DynamicResource` 使用相同的资源查找逻辑。  
  
 引用资源的其他声明方式是 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)。  
  
 特性语法是最常用于此标记扩展的语法。  在 `DynamicResource` 标识符字符串之后提供的字符串标记被指定为基础 <xref:System.Windows.DynamicResourceExtension> 扩展类的 <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> 值。  
  
 `DynamicResource` 可以在对象元素语法中使用。  在这种情况下，需要指定 <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> 属性的值。  
  
 `DynamicResource` 还可以在将 <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> 属性指定为“属性\=值”对的详细特性用法中使用：  
  
```  
<object property="{DynamicResource ResourceKey=key}" .../>  
```  
  
 如果扩展具有一个以上的可设置属性，或者某些属性是可选的，则详细用法通常会很有用。  由于 `DynamicResource` 仅有一个可设置的属性，并且此属性是必需的，因此该详细用法不具有典型性。  
  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器实现中，对此标记扩展的处理由 <xref:System.Windows.DynamicResourceExtension> 类定义。  
  
 `DynamicResource` 是标记扩展。  当要求转义属性 \(Attribute\) 值应为非文本值或非处理程序名称时，通常会实现标记扩展，相对于只在某些类型或属性 \(Property\) 上放置类型转换器而言，此要求更具有全局性。  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的所有标记扩展在其特性语法中都使用 { 和 } 字符，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器通过这一约定确认标记扩展必须处理该特性。  有关更多信息，请参见 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
## 请参阅  
 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [资源和代码](../../../../docs/framework/wpf/advanced/resources-and-code.md)   
 [x:Key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)   
 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)