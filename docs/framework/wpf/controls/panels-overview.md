---
title: "面板概述 | Microsoft Docs"
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
  - "控件, Panel"
  - "Panel 控件 [WPF], 关于 Panel 控件"
ms.assetid: f73644af-9941-4611-8754-6d4cef03fc44
caps.latest.revision: 48
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 45
---
# 面板概述
<xref:System.Windows.Controls.Panel> 元素是控制元素呈现（元素的大小、尺寸、位置及其子内容的排列）的组件。  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供若干预定义的 <xref:System.Windows.Controls.Panel> 元素以及用来构造自定义 <xref:System.Windows.Controls.Panel> 元素的功能。  
  
 本主题包括以下部分。  
  
-   [Panel 类](#Panels_view_from_10000_feet)  
  
-   [Panel 元素公共成员](#Panels_declared_members)  
  
-   [派生的 Panel 元素](#Panels_derived_elements)  
  
-   [用户界面面板](#Panels_main_UI_elements)  
  
-   [嵌套的 Panel 元素](#Panels_nested_panel_elements)  
  
-   [自定义 Panel 元素](#Panels_custom_panel_elements)  
  
-   [本地化\/全球化支持](#Panels_global_localization)  
  
-   [相关主题](#seeAlsoToggle)  
  
<a name="Panels_view_from_10000_feet"></a>   
## Panel 类  
 <xref:System.Windows.Controls.Panel> 是在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中提供布局支持的所有元素的基类。  派生的 <xref:System.Windows.Controls.Panel> 元素用于定位和排列 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 和代码中的元素。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 包括一个由派生的面板实现组成的综合套件，用来启用许多复杂的布局。  这些派生的类公开启用大多数标准[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 方案的属性和方法。  开发人员如果找不到满足其需要的子排列行为，可以通过重写 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 和 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 方法创建新的布局。  有关自定义布局行为的更多信息，请参见[自定义 Panel 元素](#Panels_custom_panel_elements)。  
  
<a name="Panels_declared_members"></a>   
## Panel 公共成员  
 所有的 <xref:System.Windows.Controls.Panel> 元素都支持由 <xref:System.Windows.FrameworkElement> 定义的基本的大小调整和定位属性，包括 <xref:System.Windows.FrameworkElement.Height%2A>、<xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A>、<xref:System.Windows.FrameworkElement.Margin%2A> 和 <xref:System.Windows.FrameworkElement.LayoutTransform%2A>。  有关由 <xref:System.Windows.FrameworkElement> 定义的定位属性的其他信息，请参见[Alignment、Margin 和 Padding 概述](../../../../docs/framework/wpf/advanced/alignment-margins-and-padding-overview.md)。  
  
 <xref:System.Windows.Controls.Panel> 公开了其他一些属性，这些属性对于理解和使用布局至关重要。  <xref:System.Windows.Controls.Panel.Background%2A> 属性用于填充具有 <xref:System.Windows.Media.Brush> 的派生 Panel 元素的各个边界之间的区域。  <xref:System.Windows.Controls.Panel.Children%2A> 表示组成 <xref:System.Windows.Controls.Panel> 的元素的子集合。  <xref:System.Windows.Controls.Panel.InternalChildren%2A> 表示 <xref:System.Windows.Controls.Panel.Children%2A> 集合的内容以及由数据绑定生成的这些成员。  它们都由在父 <xref:System.Windows.Controls.Panel> 中承载的子元素的 <xref:System.Windows.Controls.UIElementCollection> 组成。  
  
 Panel 也公开了一个 <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=fullName> 附加属性，该属性可以用于在派生的 <xref:System.Windows.Controls.Panel> 中实现分层顺序。  面板的 <xref:System.Windows.Controls.Panel.Children%2A> 集合中 <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=fullName> 值较高的成员显示在 <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=fullName> 值较低的成员的前面。  对于如 <xref:System.Windows.Controls.Canvas> 和 <xref:System.Windows.Controls.Grid> 等面板，它们允许子元素共享相同的坐标空间的，因而这一点对它们尤其有用。  
  
 <xref:System.Windows.Controls.Panel> 还定义了 <xref:System.Windows.Controls.Panel.OnRender%2A> 方法，该方法可用于重写 <xref:System.Windows.Controls.Panel> 的默认呈现行为。  
  
#### 附加属性  
 派生的 Panel 元素广泛使用[附加的属性](GTMT)。  附加的属性是[依赖项属性](GTMT)的专用形式，它并不具有常规的[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性“wrapper”。  附加的属性具有[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中的专用语法，可从下面的几个示例中查看这一点。  
  
 附加的属性的一个用途是允许子元素存储实际已在父元素中定义的属性的唯一值。  此功能的一项应用是使子元素通知父元素前者希望在[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中显示的方式，这对于应用程序布局非常有用。  有关更多信息，请参见[附加属性概述](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)。  
  
<a name="Panels_derived_elements"></a>   
## 派生的 Panel 元素  
 许多对象都是从 <xref:System.Windows.Controls.Panel> 派生的，但并不是所有对象都会用作根布局提供程序。  为创建应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 而专门设计了六个已定义的 Panel 类（<xref:System.Windows.Controls.Canvas>、<xref:System.Windows.Controls.DockPanel>、<xref:System.Windows.Controls.Grid>、<xref:System.Windows.Controls.StackPanel>、<xref:System.Windows.Controls.VirtualizingStackPanel> 和 <xref:System.Windows.Controls.WrapPanel>）。  
  
 每个 Panel 元素均封装自己的专用功能，如下表所示。  
  
|元素名称|是否为 UI 面板？|说明|  
|----------|----------------|--------|  
|<xref:System.Windows.Controls.Canvas>|是|定义一个区域，在此区域内，您可以使用相对于 <xref:System.Windows.Controls.Canvas> 区域的坐标显式定位子元素。|  
|<xref:System.Windows.Controls.DockPanel>|是|定义一个区域，在此区域中，您可以使子元素互相水平或垂直排列。|  
|<xref:System.Windows.Controls.Grid>|是|定义由行和列组成的灵活网格区域。  可以使用 <xref:System.Windows.FrameworkElement.Margin%2A> 属性精确定位 <xref:System.Windows.Controls.Grid> 的子元素。|  
|<xref:System.Windows.Controls.StackPanel>|是|将子元素排列成一行（可沿水平或垂直方向）。|  
|<xref:System.Windows.Controls.Primitives.TabPanel>|否|处理 <xref:System.Windows.Controls.TabControl> 中选项卡按钮的布局。|  
|<xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>|否|在 <xref:System.Windows.Controls.ToolBar> 控件内排列内容。|  
|<xref:System.Windows.Controls.Primitives.UniformGrid>|否|<xref:System.Windows.Controls.Primitives.UniformGrid> 用于在网格内按全部相等的单元格大小排列子元素。|  
|<xref:System.Windows.Controls.VirtualizingPanel>|否|提供面板的一个基类，该基类能够“虚拟化”面板的子集合。|  
|<xref:System.Windows.Controls.VirtualizingStackPanel>|是|将内容排列成一行（可沿水平或垂直方向），并使内容虚拟化。|  
|<xref:System.Windows.Controls.WrapPanel>|是|<xref:System.Windows.Controls.WrapPanel> 从左至右按顺序位置定位子元素，并在包含框的边缘处将内容断开至下一行。  后续排序按照从上至下或从右至左的顺序进行，具体取决于 <xref:System.Windows.Controls.WrapPanel.Orientation%2A> 属性的值。|  
  
<a name="Panels_main_UI_elements"></a>   
## 用户界面面板  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中有下列六个可用的 Panel 类，这些类已进行优化以支持 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 方案：<xref:System.Windows.Controls.Canvas>、<xref:System.Windows.Controls.DockPanel>、<xref:System.Windows.Controls.Grid>、<xref:System.Windows.Controls.StackPanel>、<xref:System.Windows.Controls.VirtualizingStackPanel> 和 <xref:System.Windows.Controls.WrapPanel>。  这些 Panel 元素易于使用、功能众多并且足以适用于大多数应用程序。  
  
 每个派生的 <xref:System.Windows.Controls.Panel> 元素对大小调整约束的处理方式不同。  了解 <xref:System.Windows.Controls.Panel> 如何处理水平和垂直方向的约束后，即可更准确地预知布局效果。  
  
|**面板名称**|**x 维**|**y 维**|  
|--------------|-------------|-------------|  
|<xref:System.Windows.Controls.Canvas>|受内容约束|受内容约束|  
|<xref:System.Windows.Controls.DockPanel>|受约束|受约束|  
|<xref:System.Windows.Controls.StackPanel>（垂直方向）|受约束|受内容约束|  
|<xref:System.Windows.Controls.StackPanel>（水平方向）|受内容约束|受约束|  
|<xref:System.Windows.Controls.Grid>|受约束|受约束，在 <xref:System.Windows.GridUnitType> 应用到行和列的情况下除外|  
|<xref:System.Windows.Controls.WrapPanel>|受内容约束|受内容约束|  
  
 上述每个元素更为详细的说明和用法示例见下文。  
  
<a name="Panels_overview_Canvas_subsection"></a>   
### Canvas  
 通过 <xref:System.Windows.Controls.Canvas> 元素，可以根据 *x* 和 *y* 绝对坐标定位内容。  可以在唯一的位置绘制元素；或者，如果多个元素占用了相同的坐标，则这些元素在标记中的出现顺序可决定它们的绘制顺序。  
  
 <xref:System.Windows.Controls.Canvas> 对任何 <xref:System.Windows.Controls.Panel> 均提供了最灵活的布局支持。  Height 和 Width 属性用于定义画布的区域，而画布内部的元素则按照相对于父 <xref:System.Windows.Controls.Canvas> 的区域的绝对坐标分配。  可以使用四个附加的属性（<xref:System.Windows.Controls.Canvas.Left%2A?displayProperty=fullName>、<xref:System.Windows.Controls.Canvas.Top%2A?displayProperty=fullName>、<xref:System.Windows.Controls.Canvas.Right%2A?displayProperty=fullName> 和 <xref:System.Windows.Controls.Canvas.Bottom%2A?displayProperty=fullName>）在 <xref:System.Windows.Controls.Canvas> 内精确地控制对象位置，从而允许开发人员在屏幕上精确地定位和排列元素。  
  
#### 在画布内 ClipToBounds  
 <xref:System.Windows.Controls.Canvas> 可以在屏幕上的任意位置定位子元素，即使坐标位于它自己定义的 <xref:System.Windows.FrameworkElement.Height%2A> 和 <xref:System.Windows.FrameworkElement.Width%2A> 外时也是如此。  而且，<xref:System.Windows.Controls.Canvas> 不受其子元素大小的影响。  因此，绘制子元素时有可能覆盖位于父 <xref:System.Windows.Controls.Canvas> 的边框外的其他元素。  <xref:System.Windows.Controls.Canvas> 的默认行为允许在父 <xref:System.Windows.Controls.Canvas> 的边界外绘制子元素。  如果不希望发生此行为，则可将 <xref:System.Windows.UIElement.ClipToBounds%2A> 属性设置为 `true`。  这会使 <xref:System.Windows.Controls.Canvas> 裁剪到其自身的大小。  <xref:System.Windows.Controls.Canvas> 是唯一允许在其边框外绘制子元素的布局元素。  
  
 在 [Width Properties Comparison Sample](http://go.microsoft.com/fwlink/?LinkID=160050)（宽度属性比较示例）中以图形方式演示了此行为。  
  
#### 定义和使用画布  
 只需使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 或代码，即可实例化 <xref:System.Windows.Controls.Canvas>。  下面的示例演示如何使用 <xref:System.Windows.Controls.Canvas> 以绝对方式定位内容。  此代码生成三个 100 像素的正方形。  第一个正方形为红色，其左上角 \(*x, y*\) 位置指定为 \(0, 0\)。  第二个正方形为绿色，其左上角位置为 \(100, 100\)，正好在第一个正方形的右下方。  第三个正方形为蓝色，其左上角位置为 \(50, 50\)，因此包含了第一个正方形的右下方的四分之一和第二个正方形的左上方的四分之一。  由于第三个正方形是最后放置的，因此它出现在其他两个正方形上面，也就是说，重叠部分采用第三个正方形的颜色。  
  
 [!code-csharp[CanvasOvwSample#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasOvwSample/CSharp/Canvas_Ovw_Sample.cs#1)]
 [!code-vb[CanvasOvwSample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasOvwSample/VisualBasic/canvas_vb.vb#1)]
 [!code-xml[CanvasOvwSample#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/CanvasOvwSample/XAML/default.xaml#1)]  
  
 编译后的应用程序将生成如下所示的新 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
 ![典型的 Canvas 元素。](../../../../docs/framework/wpf/controls/media/panel-intro-canvas.png "panel\_intro\_canvas")  
  
<a name="Panels_overview_DockPanel_subsection"></a>   
### DockPanel  
 <xref:System.Windows.Controls.DockPanel> 元素使用在子内容元素中设置的 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 附加属性沿容器的边缘将内容定位。  当 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 设置为 <xref:System.Windows.Controls.Dock> 或 <xref:System.Windows.Controls.Dock> 时，该属性会将子元素定位在彼此的上方或下方。  当 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 设置为 <xref:System.Windows.Controls.Dock> 或 <xref:System.Windows.Controls.Dock> 时，该属性会将子元素定位在彼此的左边或右边。  <xref:System.Windows.Controls.DockPanel.LastChildFill%2A> 属性可确定作为 <xref:System.Windows.Controls.DockPanel> 的子元素添加的最终元素的位置。  
  
 可以使用 <xref:System.Windows.Controls.DockPanel> 定位一组相关控件，如一组按钮。  也可以使用它来创建一个与 [!INCLUDE[TLA#tla_outlook](../../../../includes/tlasharptla-outlook-md.md)] 中的用户界面类似的“paned”[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
#### 根据内容调整大小  
 如果未指定 <xref:System.Windows.Controls.DockPanel> 的 <xref:System.Windows.FrameworkElement.Height%2A> 和 <xref:System.Windows.FrameworkElement.Width%2A> 属性，它会调整到其内容的大小。  它的大小可以增加或减少来适合子元素的大小。  但是，当已指定这些属性且不再有空间容纳下一个指定子元素时，<xref:System.Windows.Controls.DockPanel> 将不会显示该子元素或其后的子元素，并且不会计算其后的子元素。  
  
#### LastChildFill  
 默认情况下，<xref:System.Windows.Controls.DockPanel> 元素的最后一个子项将“填满”剩余的未分配空间。  如果不希望发生此行为，请将 <xref:System.Windows.Controls.DockPanel.LastChildFill%2A> 属性设置为 `false`。  
  
#### 定义和使用 DockPanel  
 下面的示例演示如何使用 <xref:System.Windows.Controls.DockPanel> 对空间进行分区。  添加了五个 <xref:System.Windows.Controls.Border> 元素，作为父 <xref:System.Windows.Controls.DockPanel> 的子元素。  每个元素使用 <xref:System.Windows.Controls.DockPanel> 的一个不同定位属性来对空间进行分区。  最后的元素将“填满”剩余的未分配空间。  
  
 [!code-cpp[DockPanelOvwSample#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DockPanelOvwSample/CPP/DockPanel_Ovw_Sample.cpp#1)]
 [!code-csharp[DockPanelOvwSample#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DockPanelOvwSample/CSharp/DockPanel_Ovw_Sample.cs#1)]
 [!code-vb[DockPanelOvwSample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelOvwSample/VisualBasic/dockpanel_vb.vb#1)]
 [!code-xml[DockPanelOvwSample#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DockPanelOvwSample/XAML/default.xaml#1)]  
  
 编译后的应用程序将生成如下所示的新 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
 ![典型的 DockPanel 方案。](../../../../docs/framework/wpf/controls/media/panel-intro-dockpanel.png "panel\_intro\_dockpanel")  
  
<a name="Panels_overview_Grid_subsection"></a>   
### 网格  
 <xref:System.Windows.Controls.Grid> 元素合并了绝对定位功能和表格数据控件。  使用 <xref:System.Windows.Controls.Grid> 可以轻松地定位元素和设置元素的样式。  使用 <xref:System.Windows.Controls.Grid> 可以定义灵活的行和列分组，甚至提供一种机制以共享多个 <xref:System.Windows.Controls.Grid> 元素之间的大小调整信息。  
  
#### 网格和表有什么区别？  
 <xref:System.Windows.Documents.Table> 和 <xref:System.Windows.Controls.Grid> 共享某些通用功能，但二者分别最适用于不同的方案。  <xref:System.Windows.Documents.Table> 旨在在流内容内使用（有关流内容的更多信息，请参见[流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)）。  网格最适合在表单中（主要在流内容以外的任意位置）使用。  在 <xref:System.Windows.Documents.FlowDocument> 内，<xref:System.Windows.Documents.Table> 支持流内容行为（例如分页、列回流和内容选择），而 <xref:System.Windows.Controls.Grid> 则不支持这样的行为。  另一方面，<xref:System.Windows.Controls.Grid> 最适合在 <xref:System.Windows.Documents.FlowDocument> 之外使用，原因有多种，包括 <xref:System.Windows.Controls.Grid> 根据行和列索引添加元素，而 <xref:System.Windows.Documents.Table> 则不适合。  使用 <xref:System.Windows.Controls.Grid> 元素可以对子内容进行分层，从而允许多个元素共存于单个“单元格”内。<xref:System.Windows.Documents.Table> 不支持分层。  <xref:System.Windows.Controls.Grid> 的子元素可相对于其“单元格”边界区域进行绝对定位。  <xref:System.Windows.Documents.Table> 不支持此功能。  最后，<xref:System.Windows.Controls.Grid> 与 <xref:System.Windows.Documents.Table> 相比较为轻量。  
  
#### 列和行的大小调整行为  
 在 <xref:System.Windows.Controls.Grid> 中定义的行和列可以利用 <xref:System.Windows.GridUnitType> 大小调整功能按比例分配剩余空间。  当选择 <xref:System.Windows.GridUnitType> 作为行或列的高度或宽度时，该行或列将得到一个剩余可用空间的加权比例分配。  这与 <xref:System.Windows.GridUnitType> 相反，后者将基于行或列中所含内容的大小平均分配空间。  当使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 时，此值表示为 `*` 或 `2*`。  在第一种情况下，行或列将得到一倍的可用空间；在第二种情况下，行或列将得到两倍的可用空间，依此类推。  通过将按比例分配空间的这种方法与 `Stretch` 的 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 和 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 值结合使用，可以按屏幕空间的百分比划分布局空间。  <xref:System.Windows.Controls.Grid> 是唯一可以按这种方式分配空间的布局面板。  
  
#### 定义和使用网格  
 下面的示例演示如何生成 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，并且该界面与单击 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 的“开始”菜单，然后打开“运行”对话框时看到的界面相似。  
  
 [!code-csharp[GridRunDialog#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridRunDialog/CSharp/window1.xaml.cs#1)]
 [!code-vb[GridRunDialog#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GridRunDialog/VisualBasic/grid_vb.vb#1)]  
  
 编译后的应用程序将生成如下所示的新 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
 ![典型的网格元素。](../../../../docs/framework/wpf/controls/media/avalon-run-dialog.png "avalon\_run\_dialog")  
  
<a name="Panels_overview_StackPanel_subsection"></a>   
### StackPanel  
 使用 <xref:System.Windows.Controls.StackPanel> 可以按分配的方向“堆积”元素。  默认堆积方向为垂直方向。  <xref:System.Windows.Controls.StackPanel.Orientation%2A> 属性可用于控制内容流。  
  
#### StackPanel vs.DockPanel  
 尽管 <xref:System.Windows.Controls.DockPanel> 也可以“堆积”子元素，但 <xref:System.Windows.Controls.DockPanel> 和 <xref:System.Windows.Controls.StackPanel> 在某些使用方案中并不会生成相似的结果。  例如，子元素的顺序可能会影响 <xref:System.Windows.Controls.DockPanel> 中子元素的大小，但不会影响 <xref:System.Windows.Controls.StackPanel> 中子元素的大小。  这是因为 <xref:System.Windows.Controls.StackPanel> 在堆积的 <xref:System.Double.PositiveInfinity> 方向计算大小，而 <xref:System.Windows.Controls.DockPanel> 只计算可用大小。  
  
 下面的示例演示这一主要差异。  
  
 [!code-cpp[StackPanelOvw4#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/StackPanelOvw4/CPP/StackPanel_Ovw_Sample4.cpp#1)]
 [!code-csharp[StackPanelOvw4#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StackPanelOvw4/CSharp/StackPanel_Ovw_Sample4.cs#1)]
 [!code-vb[StackPanelOvw4#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelOvw4/VisualBasic/StackPanelSamp.vb#1)]
 [!code-xml[StackPanelOvw4#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/StackPanelOvw4/XAML/default.xaml#1)]  
  
 从此图像可以看出呈现行为的区别。  
  
 ![屏幕快照：StackPanel 与DockPanel 屏幕快照](../../../../docs/framework/wpf/controls/media/layout-smiley-stackpanel.png "layout\_smiley\_stackpanel")  
  
#### 定义和使用 StackPanel  
 下面的示例演示如何使用 <xref:System.Windows.Controls.StackPanel> 创建一组垂直放置的按钮。  如果希望水平放置，请将 <xref:System.Windows.Controls.StackPanel.Orientation%2A> 属性设置为 <xref:System.Windows.Controls.Orientation>。  
  
 [!code-csharp[StackPanel_ovw2#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StackPanel_ovw2/CSharp/StackPanel_Ovw_Sample2.cs#1)]
 [!code-vb[StackPanel_ovw2#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanel_ovw2/VisualBasic/StackPanelOvw.vb#1)]  
  
 编译后的应用程序将生成如下所示的新 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
 ![典型的 StackPanel 元素。](../../../../docs/framework/wpf/controls/media/panel-intro-stackpanel.png "panel\_intro\_stackpanel")  
  
<a name="Panels_overview_VirtualizingStackPanel_subsection"></a>   
#### VirtualizingStackPanel  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还提供 <xref:System.Windows.Controls.StackPanel> 元素的一个变体，用于自动“虚拟化”数据绑定子级内容。  在此上下文中，“虚拟化”一词指的是一种方法：通过此方法根据屏幕上哪些项可见，从较多的数据项中生成一个元素子集。  如果在指定时刻只有少量 UI 元素位于屏幕上，则此时生成大量元素对于内存和处理器来说都需要进行大量处理。  <xref:System.Windows.Controls.VirtualizingStackPanel>（通过 <xref:System.Windows.Controls.VirtualizingPanel> 提供的功能）计算可见项，并与来自 <xref:System.Windows.Controls.ItemsControl>（如 <xref:System.Windows.Controls.ListBox> 或 <xref:System.Windows.Controls.ListView>）的 <xref:System.Windows.Controls.ItemContainerGenerator> 协同工作，以便仅为可见项创建元素。  
  
 <xref:System.Windows.Controls.VirtualizingStackPanel> 元素会自动设置为控件（如 <xref:System.Windows.Controls.ListBox>）的项宿主。  当承载数据绑定集合时，只要内容位于 <xref:System.Windows.Controls.ScrollViewer> 的绑定之内，就会自动对内容进行虚拟化。  在承载许多子项时，这一点可以极大地提高性能。  
  
 下面的标记演示了如何使用 <xref:System.Windows.Controls.VirtualizingStackPanel> 作为项宿主。  <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A?displayProperty=fullName> [附加的属性](GTMT)必须设置为 `true`（默认值）才能进行虚拟化。  
  
 [!code-xml[VirtualizingStackPanel_Intro#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VirtualizingStackPanel_Intro/CS/default.xaml#1)]  
  
<a name="Panels_overview_WrapPanel"></a>   
### WrapPanel  
 <xref:System.Windows.Controls.WrapPanel> 用于从左至右按顺序定位子元素，并在到达其父容器的边缘时将内容断开至下一行。  内容的方向可以是水平的，也可以是垂直的。  <xref:System.Windows.Controls.WrapPanel> 对于简单流处理 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 方案很有用。  它还可用于对其所有子元素进行统一的大小调整。  
  
 下面的示例演示如何创建一个 <xref:System.Windows.Controls.WrapPanel> 来显示 <xref:System.Windows.Controls.Button> 控件，并且使控件在到达其容器边缘时进行换行。  
  
 [!code-cpp[WrapPanel_Intro#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/WrapPanel_Intro/CPP/WrapPanel_Code.cpp#1)]
 [!code-csharp[WrapPanel_Intro#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WrapPanel_Intro/CSharp/WrapPanel_Code.cs#1)]
 [!code-vb[WrapPanel_Intro#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WrapPanel_Intro/VisualBasic/WrapPanel_vb.vb#1)]
 [!code-xml[WrapPanel_Intro#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/WrapPanel_Intro/XAML/default.xaml#1)]  
  
 编译后的应用程序将生成如下所示的新 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
 ![典型的 WrapPanel 元素。](../../../../docs/framework/wpf/controls/media/wrappanel-element.png "WrapPanel\_Element")  
  
<a name="Panels_nested_panel_elements"></a>   
## 嵌套的 Panel 元素  
 <xref:System.Windows.Controls.Panel> 元素可以彼此嵌套来生成复杂的布局。  当 <xref:System.Windows.Controls.Panel> 非常适合作为 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的一部分时，这一点是非常有用的，但可能不会满足多个 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 不同部分的需要。  
  
 对于您的应用程序可以支持的嵌套数量，并没有实际限制。不过，通常最好限制应用程序仅使用您的预期布局确实需要的那些面板。  在很多情况下，可以使用 <xref:System.Windows.Controls.Grid> 元素来代替嵌套面板，因为前者作为布局容器具有一定的灵活性。  在应用程序中使用此元素时，此元素可以将不必要的元素排除在树之外，从而可以提高应用程序的性能。  
  
 下面的示例演示如何创建一个 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，在其中利用嵌套的 <xref:System.Windows.Controls.Panel> 元素实现特定布局。  在这种特定情况下，<xref:System.Windows.Controls.DockPanel> 元素用于提供 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 结构，而嵌套的 <xref:System.Windows.Controls.StackPanel> 元素（<xref:System.Windows.Controls.Grid> 和 <xref:System.Windows.Controls.Canvas>）用于在父 <xref:System.Windows.Controls.DockPanel> 内精确定位子元素。  
  
 [!code-csharp[Nested_Panels#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Nested_Panels/CSharp/nestedpanels.cs#1)]
 [!code-vb[Nested_Panels#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Nested_Panels/VisualBasic/nestedpanels.vb#1)]  
  
 编译后的应用程序将生成如下所示的新 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
 ![利用嵌套面板的 UI。](../../../../docs/framework/wpf/controls/media/nested-panels.png "nested\_panels")  
  
<a name="Panels_custom_panel_elements"></a>   
## 自定义 Panel 元素  
 由于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一组灵活的布局控件，因此也可以通过重写 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 和 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 方法实现自定义布局行为。  可以在这些重写方法内定义新的定位行为来实现自定义的大小调整和定位。  
  
 同样，可以通过重写派生类（如 <xref:System.Windows.Controls.Canvas> 或 <xref:System.Windows.Controls.Grid>）的 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 和 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 方法来基于派生类定义自定义布局行为。  
  
 下面的标记演示如何创建自定义 <xref:System.Windows.Controls.Panel> 元素。  这个新的 <xref:System.Windows.Controls.Panel>（定义为 `PlotPanel`）支持通过使用硬编码的 *x* 和 *y* 坐标来定位子元素。  在此示例中，<xref:System.Windows.Shapes.Rectangle> 元素（未显示）定位于绘制点 50 \(*x*\) 和 50 \(*y*\)。  
  
 [!code-cpp[PlotPanel#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PlotPanel/CPP/PlotPanel.cpp#1)]
 [!code-csharp[PlotPanel#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PlotPanel/CSharp/PlotPanel.cs#1)]
 [!code-vb[PlotPanel#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PlotPanel/VisualBasic/PlotPanel.vb#1)]  
  
 若要查看更复杂的自定义面板实现，请参见 [Create a Custom Content\-Wrapping Panel Sample](http://go.microsoft.com/fwlink/?LinkID=159979)（创建自定义内容包装面板示例）。  
  
<a name="Panels_global_localization"></a>   
## 本地化\/全球化支持  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 支持的许多功能可帮助创建可本地化的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
 所有 Panel 元素本身支持 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性，该属性可用于根据用户的区域设置或语言设置动态重新流动内容。  有关更多信息，请参见 <xref:System.Windows.FrameworkElement.FlowDirection%2A>。  
  
 <xref:System.Windows.Window.SizeToContent%2A> 属性提供了一种机制，该机制使应用程序开发人员可以预料本地化的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的需要。  通过使用此属性的 <xref:System.Windows.SizeToContent> 值，父 <xref:System.Windows.Window> 始终可以动态地进行大小调整以适合内容，而且不受人为的高度或宽度限制的制约。  
  
 <xref:System.Windows.Controls.DockPanel>、<xref:System.Windows.Controls.Grid> 和 <xref:System.Windows.Controls.StackPanel> 都是实现可本地化的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的良好选择。  但 <xref:System.Windows.Controls.Canvas> 不适合这一点，因为它以绝对方式定位内容，使得难以进行本地化。  
  
 有关创建具有可本地化的[!INCLUDE[TLA#tla_ui#plural](../../../../includes/tlasharptla-uisharpplural-md.md)] 的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序的更多信息，请参见[使用自动布局概述](../../../../docs/framework/wpf/advanced/use-automatic-layout-overview.md)。  
  
## 请参阅  
 [演练：开始使用 WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)   
 [WPF Layout Gallery Sample](http://go.microsoft.com/fwlink/?LinkID=160054)   
 [布局](../../../../docs/framework/wpf/advanced/layout.md)   
 [WPF Controls Gallery Sample](http://go.microsoft.com/fwlink/?LinkID=160053)   
 [Alignment、Margin 和 Padding 概述](../../../../docs/framework/wpf/advanced/alignment-margins-and-padding-overview.md)   
 [Create a Custom Content\-Wrapping Panel Sample](http://go.microsoft.com/fwlink/?LinkID=159979)   
 [附加属性概述](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)   
 [使用自动布局概述](../../../../docs/framework/wpf/advanced/use-automatic-layout-overview.md)   
 [布局和设计](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)