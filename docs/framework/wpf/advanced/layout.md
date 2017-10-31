---
title: "布局 | Microsoft Docs"
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
  - "控件 [WPF], 布局系统"
  - "布局系统 [WPF]"
  - "WPF 布局系统"
ms.assetid: 3eecdced-3623-403a-a077-7595453a9221
caps.latest.revision: 31
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 30
---
# 布局
本主题描述 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 布局系统。  了解在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中创建用户界面时如何以及何时进行布局计算是非常重要的。  
  
 本主题包含以下各节：  
  
-   [元素边界框](#LayoutSystem_BoundingBox)  
  
-   [布局系统](#LayoutSystem_Overview)  
  
-   [测量和排列子控件](#LayoutSystem_Measure_Arrange)  
  
-   [面板元素和自定义布局行为](#LayoutSystem_PanelsCustom)  
  
-   [布局性能注意事项](#LayoutSystem_Performance)  
  
-   [子像素呈现和布局舍入](#LayoutSystem_LayoutRounding)  
  
-   [接下来的内容](#LayoutSystem_whatsnext)  
  
<a name="LayoutSystem_BoundingBox"></a>   
## 元素边界框  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中构思布局时，了解环绕所有元素的边界框非常重要。  布局系统使用的每个 <xref:System.Windows.FrameworkElement> 可以被视为是嵌入到布局中的矩形。  <xref:System.Windows.Controls.Primitives.LayoutInformation> 类返回元素布局分配的边界或槽。  矩形的大小是通过计算可用屏幕空间、任意约束的大小、布局特定属性（如边距和填充）及父 <xref:System.Windows.Controls.Panel> 元素的个别行为来确定的。  通过处理此数据，布局系统将能够计算特定 <xref:System.Windows.Controls.Panel> 的所有子级的位置。  牢记在父元素上定义的大小调整特性（如 <xref:System.Windows.Controls.Border>）会影响其子级，这非常重要。  
  
 下图显示了一个简单的布局。  
  
 ![未添加边界框的典型网格。](../../../../docs/framework/wpf/advanced/media/boundingbox1.png "boundingbox1")  
  
 可以使用以下 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 来实现此布局。  
  
 [!code-xml[LayoutInformation#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml#1)]  
  
 单独的 <xref:System.Windows.Controls.TextBlock> 元素是在 <xref:System.Windows.Controls.Grid> 内承载的。  而文本仅填充第一列的左上角，为 <xref:System.Windows.Controls.TextBlock> 分配的空间实际上要大得多。  可以使用 <xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A> 方法检索任意 <xref:System.Windows.FrameworkElement> 的边界框。  下图显示了 <xref:System.Windows.Controls.TextBlock> 元素的边界框。  
  
 ![TextBlock 的边界框现在可见。](../../../../docs/framework/wpf/advanced/media/boundingbox2.png "boundingbox2")  
  
 如黄色矩形所示，为 <xref:System.Windows.Controls.TextBlock> 元素分配的空间实际上远远大于其显示的空间。  由于还有其他元素添加到 <xref:System.Windows.Controls.Grid>，此分配可能会收缩或扩展，这取决于所添加元素的类型和大小。  
  
 可以使用 <xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A> 方法将 <xref:System.Windows.Controls.TextBlock> 的布局槽转换为 <xref:System.Windows.Shapes.Path>。  此方法对于显示元素的边界框非常有用。  
  
 [!code-csharp[LayoutInformation#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml.cs#2)]
 [!code-vb[LayoutInformation#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/LayoutInformation/VisualBasic/Window1.xaml.vb#2)]  
  
<a name="LayoutSystem_Overview"></a>   
## 布局系统  
 简单地说，布局是一个递归系统，实现对元素进行大小调整、定位和绘制。  更具体地说，布局描述对 <xref:System.Windows.Controls.Panel> 元素的 <xref:System.Windows.Controls.Panel.Children%2A> 集合的成员执行的测量和排列过程。  布局是一个计算密集型过程。  <xref:System.Windows.Controls.Panel.Children%2A> 集合越大，必须执行的计算次数就越多。  根据拥有该集合的 <xref:System.Windows.Controls.Panel> 元素所定义的布局行为，还可能会增加复杂性。  相对简单的 <xref:System.Windows.Controls.Panel>（如 <xref:System.Windows.Controls.Canvas>）的性能可能明显优于较为复杂的 <xref:System.Windows.Controls.Panel>（如 <xref:System.Windows.Controls.Grid>）。  
  
 每当子 <xref:System.Windows.UIElement> 改变其位置时，布局系统就可能触发一个新的处理过程。  因此，了解哪些事件会调用布局系统就很重要，因为不必要的调用可能导致应用程序性能变差。  下面描述调用布局系统时发生的过程。  
  
1.  子 <xref:System.Windows.UIElement> 通过首先测量它的核心属性来开始布局过程。  
  
2.  计算在 <xref:System.Windows.FrameworkElement> 上定义的大小调整属性，例如 <xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.Height%2A> 和 <xref:System.Windows.FrameworkElement.Margin%2A>。  
  
3.  应用特定于 <xref:System.Windows.Controls.Panel> 的逻辑，例如 <xref:System.Windows.Controls.Dock> 方向或堆栈 <xref:System.Windows.Controls.StackPanel.Orientation%2A>。  
  
4.  测量所有子级后排列内容。  
  
5.  <xref:System.Windows.Controls.Panel.Children%2A> 集合绘制到屏幕。  
  
6.  如果其他 <xref:System.Windows.Controls.Panel.Children%2A> 添加到集合、应用 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 或调用 <xref:System.Windows.UIElement.UpdateLayout%2A> 方法，会再次调用此过程。  
  
 下面的章节将更详尽地定义此过程及其调用方式。  
  
<a name="LayoutSystem_Measure_Arrange"></a>   
## 测量和排列子控件  
 布局系统为 <xref:System.Windows.Controls.Panel.Children%2A> 集合的每个成员完成两个处理过程：测量处理过程和排列处理过程。  每个子 <xref:System.Windows.Controls.Panel> 均提供自己的 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 和 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 方法，以实现自己特定的布局行为。  
  
 测量处理过程期间，将对 <xref:System.Windows.Controls.Panel.Children%2A> 集合的每个成员进行计算。  此过程将以调用 <xref:System.Windows.UIElement.Measure%2A> 方法开始。  此方法将在父 <xref:System.Windows.Controls.Panel> 元素的实现中调用，无需为要出现的布局显式调用该方法。  
  
 首先，将计算 <xref:System.Windows.UIElement> 的本机大小属性，如 <xref:System.Windows.UIElement.Clip%2A> 和 <xref:System.Windows.UIElement.Visibility%2A>。  这将生成一个名为 `constraintSize` 的传递给 <xref:System.Windows.FrameworkElement.MeasureCore%2A> 的值。  
  
 其次，会处理在 <xref:System.Windows.FrameworkElement> 上定义的框架属性，这将影响 `constraintSize` 的值。  这些属性通常描述基础 <xref:System.Windows.UIElement> 的大小调整特性，例如其 <xref:System.Windows.FrameworkElement.Height%2A>、<xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.Margin%2A> 和 <xref:System.Windows.FrameworkElement.Style%2A>。  上述每个属性均可能更改显示元素所必需的空间。  然后使用 `constraintSize` 作为参数调用 <xref:System.Windows.FrameworkElement.MeasureOverride%2A>。  
  
> [!NOTE]
>  在 <xref:System.Windows.FrameworkElement.Height%2A>、<xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.ActualHeight%2A> 和 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 的属性之间存在着差异。  例如，<xref:System.Windows.FrameworkElement.ActualHeight%2A> 属性是基于其他高度输入和布局系统的计算值。  该值是由布局系统本身基于实际呈现处理过程设置的，因此可能稍微小于属性（例如作为输入更改基础的 <xref:System.Windows.FrameworkElement.Height%2A>）的设置值。  
>   
>  由于 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 是一个计算值，因此您应该知道，作为布局系统各种操作的结果，该值可能有多次或递增的报告的更改。  布局系统可能正在计算子元素所需的测量空间、父元素的约束等。  
  
 测量处理过程的最终目标是让子级确定其 <xref:System.Windows.UIElement.DesiredSize%2A>，这是在 <xref:System.Windows.FrameworkElement.MeasureCore%2A> 调用期间发生的。  <xref:System.Windows.UIElement.DesiredSize%2A> 值由 <xref:System.Windows.UIElement.Measure%2A> 存储，以便在内容排列处理过程期间使用。  
  
 此排列处理过程将以调用 <xref:System.Windows.UIElement.Arrange%2A> 方法开始。  在排列处理过程期间，父 <xref:System.Windows.Controls.Panel> 元素生成一个代表子级边界的矩形。  该值会传递给 <xref:System.Windows.FrameworkElement.ArrangeCore%2A> 方法以便进行处理。  
  
 <xref:System.Windows.FrameworkElement.ArrangeCore%2A> 方法将计算子元素的 <xref:System.Windows.UIElement.DesiredSize%2A> 以及可能会影响元素呈现大小的任何其他边距。  <xref:System.Windows.FrameworkElement.ArrangeCore%2A> 生成 `arrangeSize`，后者传递到 <xref:System.Windows.Controls.Panel> 的 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 方法作为参数。  <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 生成子级的 `finalSize`。  最后，<xref:System.Windows.FrameworkElement.ArrangeCore%2A> 方法执行偏移属性（例如边距和对齐方式）的最终计算，并将子元素放在其布局槽内。  子级无需（且通常不会）填充整个分配空间。  然后，控件返回到父 <xref:System.Windows.Controls.Panel>，至此布局过程完成。  
  
<a name="LayoutSystem_PanelsCustom"></a>   
## 面板元素和自定义布局行为  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 包括从 <xref:System.Windows.Controls.Panel> 派生的一组元素。  这些 <xref:System.Windows.Controls.Panel> 元素可用来实现许多复杂的布局。  例如，堆栈元素可以使用 <xref:System.Windows.Controls.StackPanel> 元素方便地实现，而较为复杂和自由流动的布局可以使用 <xref:System.Windows.Controls.Canvas> 来实现。  
  
 下表概括了可用的布局 <xref:System.Windows.Controls.Panel> 元素。  
  
|面板名称|说明|  
|----------|--------|  
|<xref:System.Windows.Controls.Canvas>|定义一个区域，在此区域内，您可以使用相对于 <xref:System.Windows.Controls.Canvas> 区域的坐标显式定位子元素。|  
|<xref:System.Windows.Controls.DockPanel>|定义一个区域，在此区域中，您可以使子元素互相水平或垂直排列。|  
|<xref:System.Windows.Controls.Grid>|定义由行和列组成的灵活的网格区域。|  
|<xref:System.Windows.Controls.StackPanel>|将子元素排列成一行（可沿水平或垂直方向）。|  
|<xref:System.Windows.Controls.VirtualizingPanel>|为虚拟化其子数据集合的 <xref:System.Windows.Controls.Panel> 元素提供一个框架。  这是一个抽象类。|  
|<xref:System.Windows.Controls.WrapPanel>|从左至右按顺序位置定位子元素，在包含框的边缘处将内容断开至下一行。  后续排序按照从上至下或从右至左的顺序进行，具体取决于 <xref:System.Windows.Controls.WrapPanel.Orientation%2A> 属性的值。|  
  
 对于其所需布局不可能使用任意预定义的 <xref:System.Windows.Controls.Panel> 元素来实现的应用程序，您可以通过从 <xref:System.Windows.Controls.Panel> 继承并重写 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 和 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 方法来实现自定义布局行为。  有关示例，请参见 [Custom Radial Panel Sample](http://go.microsoft.com/fwlink/?LinkID=159982)（自定义的射线面板示例）  
  
<a name="LayoutSystem_Performance"></a>   
## 布局性能注意事项  
 布局是一个递归过程。  <xref:System.Windows.Controls.Panel.Children%2A> 集合中的每个子元素会在每次调用布局系统期间得到处理。  因此，应避免在不必要时触发布局系统。  以下注意事项有助于获得更好的性能。  
  
-   应注意哪些属性值更改会强制执行布局系统的递归更新。  
  
     如果依赖项属性的值可能导致布局系统被初始化，则会使用公共标志对该依赖项属性进行标记。  <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A> 和 <xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A> 提供有关哪些属性值更改会强制执行布局系统递归更新的有用提示。  通常，任何可能影响元素边界框大小的属性应将 <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A> 标志设置为 true。  有关更多信息，请参见[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  
  
-   如有可能，应使用 <xref:System.Windows.UIElement.RenderTransform%2A> 而不要使用 <xref:System.Windows.FrameworkElement.LayoutTransform%2A>。  
  
     <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 可能是影响[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 内容的非常有用的方式。  不过，如果转换的效果无需对其他元素的位置施加影响，则最好改为使用 <xref:System.Windows.UIElement.RenderTransform%2A>，因为 <xref:System.Windows.UIElement.RenderTransform%2A> 不会调用布局系统。  <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 会应用其转换，并强制执行递归布局更新，以便获得受影响元素的新位置。  
  
-   避免不必要地调用 <xref:System.Windows.UIElement.UpdateLayout%2A>。  
  
     <xref:System.Windows.UIElement.UpdateLayout%2A> 方法强制执行递归布局更新，但常常却是不必要的。  除非您确定需要进行完整更新，否则请依赖布局系统来为您调用此方法。  
  
-   当使用大型 <xref:System.Windows.Controls.Panel.Children%2A> 集合时，请考虑使用 <xref:System.Windows.Controls.VirtualizingStackPanel> 而不是常规 <xref:System.Windows.Controls.StackPanel>。  
  
     通过虚拟化子集合，<xref:System.Windows.Controls.VirtualizingStackPanel> 仅在内存中保留当前位于父 [ViewPort](GTMT) 内的对象。  因此，在大多数情况下性能会得到极大改进。  
  
<a name="LayoutSystem_LayoutRounding"></a>   
## 子像素呈现和布局舍入  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 图形系统使用与设备无关的单元来使分辨率和设备独立。  每个与设备无关的像素都会随系统的[!INCLUDE[TLA#tla_dpi](../../../../includes/tlasharptla-dpi-md.md)] 设置自动缩放。  这支持 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序可以根据不同的 [!INCLUDE[TLA2#tla_dpi](../../../../includes/tla2sharptla-dpi-md.md)] 设置进行适当的缩放，并使应用程序可以自动识别 [!INCLUDE[TLA2#tla_dpi](../../../../includes/tla2sharptla-dpi-md.md)]。  
  
 但是，这种 [!INCLUDE[TLA2#tla_dpi](../../../../includes/tla2sharptla-dpi-md.md)] 无关性可能会因为抗锯齿而呈现出不规则的边缘。  当边缘的位置处于设备像素内而不是位于设备像素之间时，可出现这些通常显示为模糊边缘或半透明的效果边缘。  布局系统提供了一种使用布局舍入对此进行调整的方法。  布局舍入是指布局系统在布局处理过程期间舍入任何非整数像素值。  
  
 默认情况下，禁用布局舍入。  若要启用布局舍入，请将任何 <xref:System.Windows.FrameworkElement> 的 <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> 属性设置为 `true`。  因为该属性是依赖项属性，所以该值将传播到可视化树中的所有子级。  若要为整个 UI 启用布局舍入，请将根容器的 <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> 设置为 `true`。  有关示例，请参见<xref:System.Windows.FrameworkElement.UseLayoutRounding%2A>。  
  
<a name="LayoutSystem_whatsnext"></a>   
## 接下来的内容  
 了解如何测量和排列元素是理解布局的第一步。  有关可用 <xref:System.Windows.Controls.Panel> 元素的更多信息，请参见[面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)。  为更好地理解可能影响布局的各种定位属性，请参见[Alignment、Margin 和 Padding 概述](../../../../docs/framework/wpf/advanced/alignment-margins-and-padding-overview.md)。  有关自定义 <xref:System.Windows.Controls.Panel> 元素的示例，请参见 [Custom Radial Panel Sample](http://go.microsoft.com/fwlink/?LinkID=159982)（自定义的射线面板示例）。  如果您准备将布局全部放入一个轻型应用程序中，请参见[演练：开始使用 WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)。  
  
## 请参阅  
 <xref:System.Windows.FrameworkElement>   
 <xref:System.Windows.UIElement>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Alignment、Margin 和 Padding 概述](../../../../docs/framework/wpf/advanced/alignment-margins-and-padding-overview.md)   
 [布局和设计](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)