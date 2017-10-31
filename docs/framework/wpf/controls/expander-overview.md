---
title: "Expander 概述 | Microsoft Docs"
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
  - "控件, Expander"
  - "Expander 控件, 关于 Expander 控件"
ms.assetid: 877bf425-0e54-49ec-8fd2-13a211377abb
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Expander 概述
利用 <xref:System.Windows.Controls.Expander> 控件可以在类似于窗口并包括标题的可展开区域中提供内容。  
  
   
  
<a name="CreatinganExpanderinXAML"></a>   
## 创建简单的 Expander  
 下面的示例演示如何创建一个简单的 <xref:System.Windows.Controls.Expander> 控件。  此示例将创建一个与上图类似的 <xref:System.Windows.Controls.Expander>。  
  
 [!code-xml[ExpanderExample#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpanderExample/CSharp/Page1.xaml#2)]  
  
 <xref:System.Windows.Controls.Expander> 的 <xref:System.Windows.Controls.ContentControl.Content%2A> 和 <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> 也可以包含复杂内容，比如 <xref:System.Windows.Controls.RadioButton> 和 <xref:System.Windows.Controls.Image> 对象。  
  
<a name="SettingtheDirectionoftheExpandingWindow"></a>   
## 设置展开内容区域的方向  
 通过使用 <xref:System.Windows.Controls.ExpandDirection> 属性，您可以将 <xref:System.Windows.Controls.Expander> 控件的内容区域设置为在四个方向的其中一个方向上展开（<xref:System.Windows.Controls.ExpandDirection>、<xref:System.Windows.Controls.ExpandDirection>、<xref:System.Windows.Controls.ExpandDirection> 或 <xref:System.Windows.Controls.ExpandDirection>）。  内容区域处于折叠状态时，只会显示 <xref:System.Windows.Controls.Expander> <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> 及其切换按钮。  将使用显示方向箭头的 <xref:System.Windows.Controls.Button> 控件作为展开或折叠内容区域的切换按钮。  在展开时，<xref:System.Windows.Controls.Expander> 将尝试在一个类似于窗口的区域中显示它的所有内容。  
  
<a name="SettingSizeDimensionsonanExpanderinaPanel"></a>   
## 在面板中控制 Expander 的大小  
 如果 <xref:System.Windows.Controls.Expander> 控件位于从 <xref:System.Windows.Controls.Panel>（如 <xref:System.Windows.Controls.StackPanel>）继承的布局控件的内部，当 <xref:System.Windows.Controls.Expander.ExpandDirection%2A> 属性设置为 <xref:System.Windows.Controls.ExpandDirection> 或 <xref:System.Windows.Controls.ExpandDirection> 时，不要在 <xref:System.Windows.Controls.Expander> 上指定 <xref:System.Windows.FrameworkElement.Height%2A>。  同样，当 <xref:System.Windows.Controls.Expander.ExpandDirection%2A> 属性设置为 <xref:System.Windows.Controls.ExpandDirection> 或 <xref:System.Windows.Controls.ExpandDirection> 时，不要在 <xref:System.Windows.Controls.Expander> 上指定 <xref:System.Windows.FrameworkElement.Width%2A>。  
  
 如果在 <xref:System.Windows.Controls.Expander> 控件显示展开内容的方向上设置大小维度，<xref:System.Windows.Controls.Expander> 将控制内容使用的区域，并在内容周围显示一个边框。  即使当内容处于折叠状态时，该边框也会显示。  若要设置展开内容区域的大小，请在 <xref:System.Windows.Controls.Expander> 的内容上设置大小维度，或者，如果需要滚动功能，请在封闭内容的 <xref:System.Windows.Controls.ScrollViewer> 上设置大小维度。  
  
 如果 <xref:System.Windows.Controls.Expander> 控件是 <xref:System.Windows.Controls.DockPanel> 中的最后一个元素，[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 会自动将 <xref:System.Windows.Controls.Expander> 维度设置为与 <xref:System.Windows.Controls.DockPanel> 的其余区域相等。  若要防止此默认行为，请将 <xref:System.Windows.Controls.DockPanel> 对象的 <xref:System.Windows.Controls.DockPanel.LastChildFill%2A> 属性设置为 `false`，或者确保 <xref:System.Windows.Controls.Expander> 不是 <xref:System.Windows.Controls.DockPanel> 中的最后一个元素。  
  
<a name="CreatingScrollableContent"></a>   
## 创建可滚动的内容  
 如果内容对于内容区域的大小而言太大，您可以在 <xref:System.Windows.Controls.ScrollViewer> 中换行显示 <xref:System.Windows.Controls.Expander> 的内容，以便提供可滚动的内容。  <xref:System.Windows.Controls.Expander> 控件本身未自动提供滚动功能。  下图显示了一个包含 <xref:System.Windows.Controls.ScrollViewer> 控件的 <xref:System.Windows.Controls.Expander> 控件。  
  
 **ScrollViewer 中的 Expander**  
  
 ![带有 ScrollBar 的 Expander](../../../../docs/framework/wpf/controls/media/expanderwithscrollbar.JPG "ExpanderWithScrollBar")  
  
 如果将 <xref:System.Windows.Controls.Expander> 控件放在 <xref:System.Windows.Controls.ScrollViewer> 中，请将与 <xref:System.Windows.Controls.Expander> 内容展开方向对应的 <xref:System.Windows.Controls.ScrollViewer> 维度属性设置为 <xref:System.Windows.Controls.Expander> 内容区域的大小。  例如，如果将 <xref:System.Windows.Controls.Expander> 的 <xref:System.Windows.Controls.Expander.ExpandDirection%2A> 属性设置为 <xref:System.Windows.Controls.ExpandDirection>（内容区域向下展开），请将 <xref:System.Windows.Controls.ScrollViewer> 控件的 <xref:System.Windows.FrameworkElement.Height%2A> 属性设置为内容区域的必需高度。  如果您设置的是内容本身的高度维度，<xref:System.Windows.Controls.ScrollViewer> 将无法识别此设置，并因此无法提供可滚动的内容。  
  
 下面的示例演示如何创建一个 <xref:System.Windows.Controls.Expander> 控件，该控件具有复杂内容并包含 <xref:System.Windows.Controls.ScrollViewer> 控件。  此示例将创建一个与本节开头的插图类似的 <xref:System.Windows.Controls.Expander>。  
  
 [!code-csharp[ExpanderRichContent#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml.cs#1)]
 [!code-vb[ExpanderRichContent#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpanderRichContent/VisualBasic/Window1.xaml.vb#1)]
 [!code-xml[ExpanderRichContent#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml#1)]  
  
<a name="UsingtheAlignmentProperties"></a>   
## 使用对齐方式属性  
 可以通过在 <xref:System.Windows.Controls.Expander> 控件上设置 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> 和 <xref:System.Windows.Controls.Control.VerticalContentAlignment%2A> 属性来对齐内容。  设置了这些属性后，对齐方式将应用于标题，并同时应用于展开的内容。  
  
## 请参阅  
 <xref:System.Windows.Controls.Expander>   
 <xref:System.Windows.Controls.ExpandDirection>   
 [帮助主题](../../../../docs/framework/wpf/controls/expander-how-to-topics.md)