---
title: "资源和代码 | Microsoft Docs"
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
  - "键, 使用对象作为"
  - "程序代码, 访问资源"
  - "程序代码, 创建资源"
  - "资源, 从程序代码访问"
  - "资源, 使用程序代码创建"
ms.assetid: c1cfcddb-e39c-41c8-a7f3-60984914dfae
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 资源和代码
本概述主要介绍可以如何使用代码（而非[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 语法）来访问或创建 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 资源。  有关常规资源用法以及 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 语法角度的资源的更多信息，请参见 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
   
  
<a name="accessing"></a>   
## 从代码访问资源  
 如果标识资源的键是通过 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 定义的，则这些键也用于当您在代码中请求资源时检索特定资源。  从代码检索资源的最简单方法是从应用程序中的框架级对象调用 <xref:System.Windows.FrameworkElement.FindResource%2A> 或 <xref:System.Windows.FrameworkElement.TryFindResource%2A> 方法。  这两个方法之间的行为差异在于当未找到所请求的键时所发生的情况。  <xref:System.Windows.FrameworkElement.FindResource%2A> 引发异常；<xref:System.Windows.FrameworkElement.TryFindResource%2A> 不引发异常，而是返回 `null`。  每个方法都将资源键作为一个输入参数，并返回一个松散类型的对象。  资源键通常是字符串，但有时也使用非字符串；有关详细信息，请参见[将对象用作键](#objectaskey)部分。  通常应将返回的对象强制转换为请求资源时设置的属性所要求的类型。  代码资源解决方案的查找逻辑与动态代码引用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 情况相同。  搜索资源从调用元素开始，然后继续搜索[逻辑树](GTMT)中的后续父元素。  如果必要，查找将继续向应用程序资源、主题以及系统资源进行。  资源的代码请求将正确地说明资源字典（可能排在从 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 加载的资源字典之后）中的运行时更改，也将说明实时系统资源更改。  
  
 下面是一段简短的代码示例，该示例按键查找资源并使用返回的值来设置属性，该示例是作为 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序实现的。  
  
 [!code-csharp[PropertiesOvwSupport#ResourceProceduralGet](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml.cs#resourceproceduralget)]
 [!code-vb[PropertiesOvwSupport#ResourceProceduralGet](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page3.xaml.vb#resourceproceduralget)]  
  
 分配资源引用的另一种方法是 <xref:System.Windows.FrameworkElement.SetResourceReference%2A>。  该方法采用两个参数：资源的键，以及特定依赖项属性（属于资源值要赋予的元素实例）的标识符。  此方法在功能上是相同的，且具有无需强制转换任何返回值的优点。  
  
 还有另一种以编程方式访问资源的方法，即：将 <xref:System.Windows.FrameworkElement.Resources%2A> 属性的内容作为字典来访问。  通过访问该属性包含的字典，还可以向现有集合中添加新资源、检查集合中是否已经存在给定的键名称以及执行其他字典\/集合操作。  如果完全以代码编写 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序，则也可以通过代码创建整个集合，为其指定键，然后将完成的集合指定给已建立的元素的 <xref:System.Windows.FrameworkElement.Resources%2A> 属性。  这将在下一部分介绍。  
  
 可以在任何给定的 <xref:System.Windows.FrameworkElement.Resources%2A> 集合内编制索引（将特定键用作索引），但您应当知道以这种方式访问资源不遵循资源解决方案的常规运行时规则。  您访问的仅是该特定集合。  如果在请求的键处未找到有效的对象，则资源查找将不会遍历范围直至根或应用程序。  但是，在某些情况下，正因为对键的搜索范围进行了更多的约束，才使得此方法在性能上具有优势。  有关如何直接处理资源字典的更多详细信息，请参见 <xref:System.Windows.ResourceDictionary> 类。  
  
<a name="creating"></a>   
## 使用代码创建资源  
 如果要以代码创建整个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序，您可能也需要以代码创建该应用程序中的任何资源。  要实现此目的，应当先新建一个 <xref:System.Windows.ResourceDictionary> 实例，然后使用对 <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=fullName> 的连续调用将所有资源添加到字典中。  然后使用最终创建的 <xref:System.Windows.ResourceDictionary> 来设置位于页范围内的元素的 <xref:System.Windows.FrameworkElement.Resources%2A> 属性，或设置 <xref:System.Windows.Application.Resources%2A?displayProperty=fullName> 的属性。  您也可以将 <xref:System.Windows.ResourceDictionary> 作为一个单独的对象来维护（而不将它添加到元素中）。  但是，如果这样，则您必须按项键来访问其中的资源，就好像它是泛型字典一样。  未附加到元素的 `Resources` 属性的 <xref:System.Windows.ResourceDictionary> 将不作为元素树的一部分存在，在查找序列中也不具有可供 <xref:System.Windows.FrameworkElement.FindResource%2A> 及相关方法使用的范围。  
  
<a name="objectaskey"></a>   
## 将对象用作键  
 大多数资源用法都会将资源的键设置为字符串。  但是，各个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 功能都特意不使用字符串类型来指定键，而是将此参数设置为对象。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 样式和主题支持使用按对象对资源进行键控的功能。  主题中成为非样式控件的默认样式的样式都将按它们要应用于的控件的 <xref:System.Type> 来进行键控。  按类型进行键控提供了一种可靠的查找机制，该机制作用于每个控件类型的默认实例，即使派生类型不具有默认样式，也可以通过反射检测到类型，并将类型用于设置派生类的样式。  可以使用 [x:Type 标记扩展](../../../../docs/framework/xaml-services/x-type-markup-extension.md)为 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中定义的资源指定 <xref:System.Type> 键。  对于支持 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 功能的其他非字符串键用法，也存在类似扩展，如 [ComponentResourceKey 标记扩展](../../../../docs/framework/wpf/advanced/componentresourcekey-markup-extension.md)。  
  
## 请参阅  
 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)