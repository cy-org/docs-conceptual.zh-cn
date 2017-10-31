---
title: "优化性能：对象行为 | Microsoft Docs"
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
  - "依赖项属性, 性能"
  - "事件处理程序 [WPF]"
  - "Freezable 对象, 性能"
  - "对象性能注意事项"
  - "用户界面虚拟化"
ms.assetid: 73aa2f47-1d73-439a-be1f-78dc4ba2b5bd
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 优化性能：对象行为
了解 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 对象的内部行为，有助于您在功能和性能之间做出一个适当的取舍。  
  
   
  
<a name="Not_Removing_Event_Handlers"></a>   
## 不移除对象的事件处理程序可能会使对象保持活动状态  
 对象传递给其事件的委托是对该对象的有效引用。  因此，事件处理程序可以使对象保持活动状态的时间超过预期时间。  当对已注册为侦听对象事件的对象执行清理时，在释放对象前移除委托是非常必要的。  将不需要的对象保持为活动状态会增加应用程序内存使用量。  当对象为[逻辑树](GTMT)或[可视化树](GTMT)的根时更是如此。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 为事件引入了弱事件侦听器模式，当很难跟踪源和侦听器之间的对象生存期关系时，这种模式特别有用。  某些现有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件使用此模式。  如果您正在实现带有自定义事件的对象，此模式可能对您有用。  有关详细信息，请参见 [弱事件模式](../../../../docs/framework/wpf/advanced/weak-event-patterns.md)。  
  
 有若干工具（如 CLR 探查器和工作集查看器）可以提供有关指定进程的内存使用量的信息。  CLR 探查器包括分配配置文件的一组非常有用的视图，其中包括已分配类型的直方图、分配和调用关系图、显示各代垃圾回收及上述回收之后托管堆的结果状态的时间线，以及显示每个方法分配和程序集加载的调用树。  有关更多信息，请参见 [.NET Framework Developer Center](http://msdn.microsoft.com/zh-cn/netframework/aa497289\(en-us\).aspx)（.NET Framework 开发人员中心）。  
  
<a name="DPs_and_Objects"></a>   
## 依赖项属性和对象  
 通常，访问 <xref:System.Windows.DependencyObject> 的[依赖项属性](GTMT)的速度不会慢于访问 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性的速度。  由于设置属性值会导致产生一些小额的性能系统开销，因此获取值与从 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性获取值的速度一样快。  抵销一些小的性能系统开销是因为[依赖项属性](GTMT)支持可靠的功能，如数据绑定、动画、继承和样式设置。  有关更多信息，请参见[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  
  
### DependencyProperty 优化  
 在应用程序中定义[依赖项属性](GTMT)时请务必谨慎。  如果 <xref:System.Windows.DependencyProperty> 仅影响呈现类型元数据选项，而不是其他元数据选项（如 <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A>），则您应通过重写其元数据来对其进行同样标记。  有关重写或获取属性元数据的更多信息，请参见[依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)。  
  
 如果并非所有属性更改都会实际影响测量、排列和呈现，则通过属性更改处理程序手动使测量、排列和呈现处理过程无效的做法可能会使效率更高。  例如，您可能决定仅在值大于设置的限制时才重新呈现背景。  在这种情况下，当值超过设置的限制时，您的属性更改处理程序仅会使呈现无效。  
  
### 将 DependencyProperty 设置为可继承的会影响性能  
 默认情况下，注册的[依赖项属性](GTMT)是不可继承的。  不过，您可以显式地使所有属性变为可继承的。  尽管这是一个有用的功能，但是将属性转换为可继承的会影响性能，这是因为会增加属性无效的时间长度。  
  
### 谨慎使用 RegisterClassHandler  
 调用 <xref:System.Windows.EventManager.RegisterClassHandler%2A> 会允许您保存实例状态，但是请注意将对每个实例调用处理程序，这将导致性能发生问题。  当应用程序要求您保存实例状态时，请仅使用 <xref:System.Windows.EventManager.RegisterClassHandler%2A>。  
  
### 在注册过程期间为 DependencyProperty 设置默认值  
 当创建要求默认值的 <xref:System.Windows.DependencyProperty> 时，请将传递来的默认元数据用作 <xref:System.Windows.DependencyProperty> 的 <xref:System.Windows.DependencyProperty.Register%2A> 方法的参数来设置此值。  请使用此技术，而不要在构造函数中或在元素的每个实例上设置属性值。  
  
### 使用 Register 设置 PropertyMetadata 值  
 创建 <xref:System.Windows.DependencyProperty> 时，您可以选择是使用 <xref:System.Windows.DependencyProperty.Register%2A> 还是 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> 方法来设置 <xref:System.Windows.PropertyMetadata>。  尽管您的对象可能有一个静态构造函数来调用 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A>，但这不是最佳方案，它会影响性能。  为了获得最佳的性能，请在调用 <xref:System.Windows.DependencyProperty.Register%2A> 期间设置 <xref:System.Windows.PropertyMetadata>。  
  
<a name="Freezable_Objects"></a>   
## Freezable 对象  
 <xref:System.Windows.Freezable> 是一种特殊的对象类型，具有两个状态：解冻和冻结。  尽可能地冻结对象会改进应用程序性能，并缩小其工作集。  有关更多信息，请参见 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
 每个 <xref:System.Windows.Freezable> 都具有一个 <xref:System.Windows.Freezable.Changed> 事件，当前者发生更改时将引发此事件。  不过，更改通知会极大地降低应用程序的性能。  
  
 我们以下面的示例为例，其中每个 <xref:System.Windows.Shapes.Rectangle> 都使用相同的 <xref:System.Windows.Media.Brush> 对象：  
  
 [!code-csharp[Performance#PerformanceSnippet2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet2)]
 [!code-vb[Performance#PerformanceSnippet2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet2)]  
  
 默认情况下，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 为 <xref:System.Windows.Media.SolidColorBrush> 对象的 <xref:System.Windows.Freezable.Changed> 事件提供一个事件处理程序，以便使 <xref:System.Windows.Shapes.Rectangle> 对象的 <xref:System.Windows.Shapes.Shape.Fill%2A> 属性无效。  在这种情况下，每次 <xref:System.Windows.Media.SolidColorBrush> 不得不激发其 <xref:System.Windows.Freezable.Changed> 事件时，就必须为每个 <xref:System.Windows.Shapes.Rectangle> 调用回调函数，这些回调函数调用的累积将导致性能严重下降。  此外，此时添加和删除处理程序将会严重影响性能，这是因为应用程序将不得不遍历整个列表才能执行此操作。  如果您的应用程序方案从未更改 <xref:System.Windows.Media.SolidColorBrush>，您将为不必要地维护 <xref:System.Windows.Freezable.Changed> 事件处理程序付出代价。  
  
 冻结 <xref:System.Windows.Freezable> 会改善其性能，因为它不再需要因维护更改通知而消耗资源。  下表显示了简单的 <xref:System.Windows.Media.SolidColorBrush> 在其 <xref:System.Windows.Freezable.IsFrozen%2A> 属性设置为 `true` 时的大小，并列出该属性未设置为该值时的情况以供对比。  这是假设将一个画笔应用于十个 <xref:System.Windows.Shapes.Rectangle> 对象的 <xref:System.Windows.Shapes.Shape.Fill%2A> 属性。  
  
|**省\/市\/自治区**|**大小**|  
|-------------------|------------|  
|冻结 <xref:System.Windows.Media.SolidColorBrush>|212 字节|  
|非冻结 <xref:System.Windows.Media.SolidColorBrush>|972 字节|  
  
 下面的代码示例演示了此概念：  
  
 [!code-csharp[Performance#PerformanceSnippet3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet3)]
 [!code-vb[Performance#PerformanceSnippet3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet3)]  
  
### 解冻的 Freezable 对象的已更改处理程序可以使对象保持活动状态  
 对象传递给 <xref:System.Windows.Freezable> 对象的 <xref:System.Windows.Freezable.Changed> 事件的委托是对该对象的有效引用。  因此，<xref:System.Windows.Freezable.Changed> 事件处理程序可以使对象保持活动状态的时间超过预期时间。  当对已注册为侦听 <xref:System.Windows.Freezable> 对象的 <xref:System.Windows.Freezable.Changed> 事件的对象执行清理时，在释放对象前移除该委托是非常有必要的。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还在内部挂钩 <xref:System.Windows.Freezable.Changed> 事件。  例如，所有值为 <xref:System.Windows.Freezable> 的[依赖项属性](GTMT)将自动侦听 <xref:System.Windows.Freezable.Changed> 事件。  <xref:System.Windows.Shapes.Shape.Fill%2A> 属性（带一个 <xref:System.Windows.Media.Brush>）说明了此概念。  
  
 [!code-csharp[Performance#PerformanceSnippet4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet4)]
 [!code-vb[Performance#PerformanceSnippet4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet4)]  
  
 将 `myRectangle.Fill` 赋值为 `myBrush` 时，指回 <xref:System.Windows.Shapes.Rectangle> 对象的委托将添加到 <xref:System.Windows.Media.SolidColorBrush> 对象的 <xref:System.Windows.Freezable.Changed> 事件。  这意味着以下代码实际不会使 `myRect` 可以进行垃圾回收：  
  
 [!code-csharp[Performance#PerformanceSnippet5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet5)]
 [!code-vb[Performance#PerformanceSnippet5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet5)]  
  
 在这种情况下，`myBrush` 仍会使 `myRectangle` 保持活动状态，并在其激发 <xref:System.Windows.Freezable.Changed> 事件时对其进行回调。  请注意，将新 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Shapes.Shape.Fill%2A> 属性赋值为 `myBrush` 时，仅将另一个事件处理程序添加到 `myBrush`。  
  
 清理这些类型的对象的建议方式是从 <xref:System.Windows.Shapes.Shape.Fill%2A> 属性移除 <xref:System.Windows.Media.Brush>，这将依次移除 <xref:System.Windows.Freezable.Changed> 事件处理程序。  
  
 [!code-csharp[Performance#PerformanceSnippet6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet6)]
 [!code-vb[Performance#PerformanceSnippet6](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet6)]  
  
<a name="User_Interface_Virtualization"></a>   
## 使用接口虚拟化  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还提供 <xref:System.Windows.Controls.StackPanel> 元素的一个变体，用于自动“虚拟化”数据绑定子级内容。  在此上下文中，“虚拟化”一词指的是一种方法：通过此方法根据屏幕上哪些项可见，从较多的数据项中生成一个对象子集。  如果在指定时刻只有少量 UI 元素位于屏幕上，则此时生成大量元素对于内存和处理器来说都需要进行大量处理。  <xref:System.Windows.Controls.VirtualizingStackPanel>（通过 <xref:System.Windows.Controls.VirtualizingPanel> 提供的功能）计算可见项，并与来自 <xref:System.Windows.Controls.ItemsControl>（如 <xref:System.Windows.Controls.ListBox> 或 <xref:System.Windows.Controls.ListView>）的 <xref:System.Windows.Controls.ItemContainerGenerator> 协同工作，以便仅为可见项创建元素。  
  
 作为性能优化的结果，将仅生成这些项的可见对象，或如果它们在屏幕上是可见的，则保持活动状态。  当这些可视化对象不再位于控件的可视区域时，则说明它们可能已被移除。  这不会与数据虚拟化发生混淆，数据虚拟化中的数据对象不会全部出现在本地集合中 \- 而是根据需要进行流化。  
  
 下表显示了将 5000 个 <xref:System.Windows.Controls.TextBlock> 元素添加到 <xref:System.Windows.Controls.StackPanel> 和 <xref:System.Windows.Controls.VirtualizingStackPanel> 并使其呈现所需的时间。  在此情形中，测量的时间是指从将文本字符串附加到 <xref:System.Windows.Controls.ItemsControl> 对象的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性至面板元素显示此文本字符串之间的时间。  
  
|**主机面板**|**呈现时间（毫秒）**|  
|--------------|------------------|  
|<xref:System.Windows.Controls.StackPanel>|3210|  
|<xref:System.Windows.Controls.VirtualizingStackPanel>|46|  
  
## 请参阅  
 [优化 WPF 应用程序性能](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [规划应用程序性能](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [利用硬件](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [布局和设计](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [应用程序资源](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [其他性能建议](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)