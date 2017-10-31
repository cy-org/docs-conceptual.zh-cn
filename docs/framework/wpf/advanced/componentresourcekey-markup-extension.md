---
title: "ComponentResourceKey 标记扩展 | Microsoft Docs"
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
  - "ComponentResourceKey"
  - "ComponentResourceKeyExtension"
helpviewer_keywords: 
  - "ComponentResourceKey 标记扩展"
  - "XAML, ComponentResourceKey 标记扩展"
ms.assetid: d6bcdbe6-61b3-40a7-b381-4e02185b5a85
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# ComponentResourceKey 标记扩展
为从外部程序集加载的资源定义和引用键。  这使得资源查找功能可以在程序集内指定目标类型，而不是在程序集内或类上指定显式的资源字典。  
  
## XAML 特性用法（设置键，精简版）  
  
```  
<object x:Key="{ComponentResourceKey {x:Type targetTypeName}, targetID}" .../>  
```  
  
## XAML 特性用法（设置键，详细版）  
  
```  
<object x:Key="{ComponentResourceKey TypeInTargetAssembly={x:Type targetTypeName}, ResourceID=targetID}" .../>  
```  
  
## XAML 特性用法（请求资源，精简版）  
  
```  
<object property="{DynamicResource {ComponentResourceKey {x:Type targetTypeName}, targetID}}" .../>  
```  
  
## XAML 特性用法（请求资源，详细版）  
  
```  
<object property="{DynamicResource {ComponentResourceKey TypeInTargetAssembly={x:Type targetTypeName}, ResourceID=targetID}}" .../>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`targetTypeName`|在资源程序集内定义的[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 公共类型的名称。|  
|`targetID`|资源的键。  在查找资源时，`targetID` 将与资源的 [x:Key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)类似。|  
  
## 备注  
 如上面的用法所示，{`ComponentResourceKey`} 标记扩展用法可以在下面的两个位置中找到：  
  
-   在主题资源字典内对键的定义，如控件作者提供的那样。  
  
-   当您重新模板化控件但希望使用控件主题提供的资源的属性值时，从数据集访问主题资源。  
  
 为了引用来自主题的组件资源，通常建议您使用 `{DynamicResource}`，而不是 `{StaticResource}`。  这展示在用法中。  建议使用 `{DynamicResource}`，因为用户可以更改主题本身。  如果需要最适合控制用户支持该主题的意图的组件资源，则还应使您的组件资源引用成为动态。  
  
 <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> 标识存在于实际定义资源的目标程序集内的类型。  无需知道 <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> 的确切定义位置，即可定义和使用 `ComponentResourceKey`，但是最终必须通过所引用的程序集来解析该类型。  
  
 <xref:System.Windows.ComponentResourceKey> 的常见用法是定义之后将作为类成员公开的键。  在该用法中，使用的是 <xref:System.Windows.ComponentResourceKey> 类构造函数，而不是标记扩展。  有关更多信息，请参见 <xref:System.Windows.ComponentResourceKey> 或主题[控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)的“定义和引用主题资源的键”部分。  
  
 为了建立键和引用监控资源，特性语法通常用于 `ComponentResourceKey` 标记扩展。  
  
 所显示的精简语法依赖 <xref:System.Windows.ComponentResourceKey.%23ctor%2A?displayProperty=fullName> 构造函数签名和标记扩展的定位参数用法。  给出 `targetTypeName` 和 `targetID` 的顺序非常重要。  详细语法依赖于 <xref:System.Windows.ComponentResourceKey.%23ctor%2A?displayProperty=fullName> 默认构造函数，之后将按照与对象元素上的实际特性语法类似的方式设置 <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> 和 <xref:System.Windows.ComponentResourceKey.ResourceId%2A>。  在详细语法中，属性的设置顺序无关紧要。  这两种可供选择的语法（精简和详细）的机制以及二者之间的关系在[标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md) 主题中有更详细的介绍。  
  
 从技术上讲，`targetID` 的值可以是任何对象，它不一定是字符串。  但是，WPF 中的最常见用法是使 `targetID` 值与属于字符串且此类字符串在 [XamlName 语法](../../../../docs/framework/xaml-services/xamlname-grammar.md)中有效的窗体对齐。  
  
 `ComponentResourceKey` 可以在对象元素语法中使用。  在这种情况下，必须同时指定 <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> 和 <xref:System.Windows.ComponentResourceKey.ResourceId%2A> 属性的值才能正确初始化该扩展。  
  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 读取器实现中，对此标记扩展的处理由 <xref:System.Windows.ComponentResourceKey> 类定义。  
  
 `ComponentResourceKey` 是标记扩展。  当要求转义属性 \(Attribute\) 值应为非文本值或非处理程序名称时，通常会实现标记扩展，相对于只在某些类型或属性 \(Property\) 上放置类型转换器而言，此要求更具有全局性。  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的所有标记扩展在其特性语法中都使用 { 和 } 字符，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器通过这一约定确认标记扩展必须处理该特性。  有关更多信息，请参见 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
## 请参阅  
 <xref:System.Windows.ComponentResourceKey>   
 <xref:System.Windows.Controls.ControlTemplate>   
 [控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)