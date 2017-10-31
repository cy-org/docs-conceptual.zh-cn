---
title: "优化性能：布局和设计 | Microsoft Docs"
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
  - "设计注意事项"
  - "布局处理过程"
  - "布局, 优化性能"
ms.assetid: 005f4cda-a849-448b-916b-38d14d9a96fe
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 优化性能：布局和设计
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序的设计在计算布局和验证对象引用时会产生不必要的系统开销，从而影响到性能。  对象的构造会影响到应用程序的性能特征，在运行时更是如此。  
  
 本主题提供这些方面的性能改进建议。  
  
## 布局  
 “布局处理过程”一词指测量和排列 <xref:System.Windows.Controls.Panel> 派生对象的子级集合的成员，然后在屏幕绘制它们的过程。  布局处理过程是一个数学密集型过程，即：集合中的子级数目越多，所需的计算量就越大。  例如，每当集合中的一个子 <xref:System.Windows.UIElement> 对象改变其位置时，布局系统就有可能触发一个新的处理过程。  由于对象特征与布局行为之间的关系非常紧密，因此必须了解可以调用布局系统的事件类型。  应用程序应尽可能减少不必要的布局处理过程调用，从而改善性能。  
  
 布局系统对集合中的每个子成员都完成两个处理过程：测量处理过程和排列处理过程。  每个子对象都针对 <xref:System.Windows.UIElement.Measure%2A> 和 <xref:System.Windows.UIElement.Arrange%2A> 方法提供它自己的重写实现，以提供其特定的布局行为。  简单地说，布局是一个递归系统，实现在屏幕上对元素进行大小调整、定位和绘制。  
  
-   子 <xref:System.Windows.UIElement> 对象通过首先测量它的核心属性来开始布局过程。  
  
-   计算与大小相关的、对象的 <xref:System.Windows.FrameworkElement> 属性，如 <xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.Height%2A> 和 <xref:System.Windows.FrameworkElement.Margin%2A>。  
  
-   应用特定于 <xref:System.Windows.Controls.Panel> 的逻辑，如 <xref:System.Windows.Controls.DockPanel> 的 <xref:System.Windows.Controls.DockPanel.Dock%2A> 属性，或者 <xref:System.Windows.Controls.StackPanel> 的 <xref:System.Windows.Controls.StackPanel.Orientation%2A> 属性。  
  
-   在测量所有子对象后，将排列或定位内容。  
  
-   将子对象集合绘制到屏幕上。  
  
 如果发生下列任意操作，将再次调用布局处理过程：  
  
-   向集合中添加了一个子对象。  
  
-   向子对象应用了 <xref:System.Windows.FrameworkElement.LayoutTransform%2A>。  
  
-   为子对象调用了 <xref:System.Windows.UIElement.UpdateLayout%2A> 方法。  
  
-   用影响测量或排列过程的元数据进行了标记的[依赖项属性](GTMT)的值发生更改。  
  
### 尽可能使用最有效的面板  
 布局过程的复杂性直接取决于您使用的 <xref:System.Windows.Controls.Panel> 派生元素的布局行为。  例如，<xref:System.Windows.Controls.Grid> 或 <xref:System.Windows.Controls.StackPanel> 控件提供的功能比 <xref:System.Windows.Controls.Canvas> 控件多很多。  功能大大提高的代价是性能成本也大大提高。  但是，如果您不需要 <xref:System.Windows.Controls.Grid> 控件提供的功能，则应使用成本较低的其他控件，如 <xref:System.Windows.Controls.Canvas> 或自定义面板。  
  
 有关更多信息，请参见[面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)。  
  
### 更新而不替换 RenderTransform  
 您可以更新 <xref:System.Windows.Media.Transform>，而不是将它作为 <xref:System.Windows.UIElement.RenderTransform%2A> 属性的值来替换。  当涉及动画时，此方法尤其有用。  通过更新现有的 <xref:System.Windows.Media.Transform>，可以避免启动不必要的布局计算。  
  
### 从上到下生成树  
 当在[逻辑树](GTMT)中添加或移除节点时，会在该节点的父级及其所有子级上引起属性失效。  因此，应始终遵循从上到下的构造模式，以避免因为在经过验证的节点中出现不必要的失效而为此付出代价。  下表从执行速度的角度列出了从上到下构建树与从下到上构建树之间的区别，其中树有 150 级深，并且每一级都有一个 <xref:System.Windows.Controls.TextBlock> 和 <xref:System.Windows.Controls.DockPanel>。  
  
|**操作**|**构建树（以毫秒为单位）**|**呈现 — 包括生成树（以毫秒为单位）**|  
|------------|---------------------|----------------------------|  
|从下到上|366|454|  
|从上到下|11|96|  
  
 下面的代码示例演示如何从上到下创建树。  
  
 [!code-csharp[Performance#PerformanceSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet1)]
 [!code-vb[Performance#PerformanceSnippet1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet1)]  
  
 有关逻辑树的更多信息，请参见 [WPF 中的树](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)。  
  
## 请参阅  
 [优化 WPF 应用程序性能](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [规划应用程序性能](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [利用硬件](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [对象行为](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [应用程序资源](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [其他性能建议](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)   
 [布局](../../../../docs/framework/wpf/advanced/layout.md)