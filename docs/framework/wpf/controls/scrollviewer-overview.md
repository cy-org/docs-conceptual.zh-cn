---
title: "ScrollViewer 概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "控件, ScrollViewer"
  - "ScrollViewer 控件, 关于 ScrollViewer 控件"
ms.assetid: 94a13b94-cfdf-4b12-a1aa-90cb50c6e9b9
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# ScrollViewer 概述
用户界面中的内容通常比计算机屏幕的显示区域大。  利用 <xref:System.Windows.Controls.ScrollViewer> 控件可以方便地使 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序中的内容具备滚动功能。  本主题介绍 <xref:System.Windows.Controls.ScrollViewer> 元素，并提供若干用法示例。  
  
 本主题包含以下各节：  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
-   [ScrollViewer 控件](#what_is_a_scrollviewer_element)  
  
-   [物理滚动与逻辑滚动](#scrollviewer_physical_vs_logical)  
  
-   [定义和使用 ScrollViewer 元素](#scrollviewer_markup_syntax_and_sample)  
  
-   [设置 ScrollViewer 的样式](#scrollviewer_styling_scrollviewer)  
  
-   [对文档进行分页](#scrollviewer_scroll_vs_paginate)  
  
-   [Related Topics](#seeAlsoToggle)  
  
<a name="what_is_a_scrollviewer_element"></a>   
## ScrollViewer 控件  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中有两个具备滚动功能的预定义元素：<xref:System.Windows.Controls.Primitives.ScrollBar> 和 <xref:System.Windows.Controls.ScrollViewer>。  <xref:System.Windows.Controls.ScrollViewer> 控件封装了水平和垂直 <xref:System.Windows.Controls.Primitives.ScrollBar> 元素以及一个内容容器（如 <xref:System.Windows.Controls.Panel> 元素），以便在可滚动的区域中显示其他可见元素。  您必须建立自定义对象才能使用 <xref:System.Windows.Controls.Primitives.ScrollBar> 元素实现内容滚动。  不过，您可以单独使用 <xref:System.Windows.Controls.ScrollViewer> 元素，因为它是一个封装了 <xref:System.Windows.Controls.Primitives.ScrollBar> 功能的复合控件。  
  
 <xref:System.Windows.Controls.ScrollViewer> 控件既响应鼠标命令，也响应键盘命令，并定义了许多可用于按预设的增量滚动内容的方法。  可以使用 <xref:System.Windows.Controls.ScrollViewer.ScrollChanged> 事件来检测 <xref:System.Windows.Controls.ScrollViewer> 状态的更改。  
  
 <xref:System.Windows.Controls.ScrollViewer> 只能有一个子级，通常可为 <xref:System.Windows.Controls.Panel> 元素，该元素可承载元素的 <xref:System.Windows.Controls.Panel.Children%2A> 集合。  <xref:System.Windows.Controls.ContentPresenter.Content%2A> 属性定义 <xref:System.Windows.Controls.ScrollViewer> 的唯一子项。  
  
<a name="scrollviewer_physical_vs_logical"></a>   
## 物理滚动与逻辑滚动  
 物理滚动用于按预设的物理增量（通常按以像素为单位声明的值）滚动内容。  逻辑滚动用于滚动到逻辑树中的下一项。  物理滚动是大多数 <xref:System.Windows.Controls.Panel> 元素的默认滚动行为。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 同时支持这两种类型的滚动。  
  
#### IScrollInfo 接口  
 <xref:System.Windows.Controls.Primitives.IScrollInfo> 接口表示 <xref:System.Windows.Controls.ScrollViewer> 或派生控件内的主滚动区域。  该接口定义可由 <xref:System.Windows.Controls.Panel> 元素实现的滚动属性和方法，这些元素需要按逻辑单位（而不是按物理增量）滚动。  通过将 <xref:System.Windows.Controls.Primitives.IScrollInfo> 的实例转换为派生的 <xref:System.Windows.Controls.Panel>，然后使用其滚动方法，从而提供了一种有用的方法，可以滚动到子集合中的下一个逻辑单位，而不是按像素增量滚动。  默认情况下，<xref:System.Windows.Controls.ScrollViewer> 控件支持按物理单位滚动。  
  
 <xref:System.Windows.Controls.StackPanel> 和 <xref:System.Windows.Controls.VirtualizingStackPanel> 都实现了 <xref:System.Windows.Controls.Primitives.IScrollInfo>，并以本机方式支持逻辑滚动。  对于以本机方式支持逻辑滚动的布局控件，您仍然可以通过将宿主 <xref:System.Windows.Controls.Panel> 元素放在 <xref:System.Windows.Controls.ScrollViewer> 中并将 <xref:System.Windows.Controls.ScrollViewer.CanContentScroll%2A> 属性设置为 `false` 来实现物理滚动。  
  
 下面的代码示例演示如何将 <xref:System.Windows.Controls.Primitives.IScrollInfo> 的实例转换为 <xref:System.Windows.Controls.StackPanel>，并使用接口定义的内容滚动方法（<xref:System.Windows.Controls.Primitives.IScrollInfo.LineUp%2A> 和 <xref:System.Windows.Controls.Primitives.IScrollInfo.LineDown%2A>）。  
  
 [!code-csharp[IScrollInfoMethods#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml.cs#3)]
 [!code-vb[IScrollInfoMethods#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/IScrollInfoMethods/VisualBasic/Window1.xaml.vb#3)]  
  
<a name="scrollviewer_markup_syntax_and_sample"></a>   
## 定义和使用 ScrollViewer 元素  
 下面的示例在包含某些文本和一个矩形的窗口中创建 <xref:System.Windows.Controls.ScrollViewer>。  <xref:System.Windows.Controls.Primitives.ScrollBar> 元素只有在需要时才会出现。  当您调整窗口大小时，由于 <xref:System.Windows.Controls.ScrollViewer.ComputedHorizontalScrollBarVisibility%2A> 和 <xref:System.Windows.Controls.ScrollViewer.ComputedVerticalScrollBarVisibility%2A> 属性更新了值，<xref:System.Windows.Controls.Primitives.ScrollBar> 元素将出现然后消失。  
  
 [!code-cpp[ScrollViewer#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/ScrollViewer/CPP/ScrollViewer_wcp.cpp#1)]
 [!code-csharp[ScrollViewer#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewer/CSharp/ScrollViewer_wcp.cs#1)]
 [!code-vb[ScrollViewer#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ScrollViewer/VisualBasic/ScrollViewer.vb#1)]
 [!code-xml[ScrollViewer#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/ScrollViewer/XAML/Pane1.xaml#1)]  
  
<a name="scrollviewer_styling_scrollviewer"></a>   
## 设置 ScrollViewer 的样式  
 像 Windows Presentation Foundation 中的所有控件一样，可以设置 <xref:System.Windows.Controls.ScrollViewer> 的样式以便更改该控件的默认呈现行为。  有关控件样式设置的附加信息，请参见[样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。  
  
<a name="scrollviewer_scroll_vs_paginate"></a>   
## 对文档进行分页  
 对于文档内容，一种替代滚动的方法是选择支持分页的文档容器。  <xref:System.Windows.Documents.FlowDocument> 适用于设计为承载于查看控件（例如 <xref:System.Windows.Controls.FlowDocumentPageViewer>）内的文档，该控件支持跨多个页面的内容分页，从而无需进行滚动。  <xref:System.Windows.Controls.DocumentViewer> 提供了一个用于查看 <xref:System.Windows.Documents.FixedDocument> 内容的解决方案，该解决方案使用传统的滚动来显示超出显示区域范围的内容。  
  
 有关文档格式和表示形式选项的附加信息，请参见 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)。  
  
## 请参阅  
 <xref:System.Windows.Controls.ScrollViewer>   
 <xref:System.Windows.Controls.Primitives.ScrollBar>   
 <xref:System.Windows.Controls.Primitives.IScrollInfo>   
 [Create a Scroll Viewer](http://msdn.microsoft.com/zh-cn/c8e46af7-b417-441b-aa30-791cbdbd43ef)   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [ScrollBar 样式和模板](../../../../docs/framework/wpf/controls/scrollbar-styles-and-templates.md)   
 [控件](../../../../docs/framework/wpf/advanced/optimizing-performance-controls.md)