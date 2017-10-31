---
title: "Alignment、Margin 和 Padding 概述 | Microsoft Docs"
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
  - "对齐"
  - "类, FrameworkElement"
  - "FrameworkElement 类"
  - "边距"
  - "填充"
ms.assetid: 9c6a2009-9b86-4e40-8605-0a2664dc3973
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Alignment、Margin 和 Padding 概述
<xref:System.Windows.FrameworkElement> 类公开一些用于精确定位子元素的属性。  本主题论述其中四个最重要的属性：<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>、<xref:System.Windows.FrameworkElement.Margin%2A>、<xref:System.Windows.Controls.Border.Padding%2A> 和 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>。  务必要了解这些属性的作用，因为这些属性是控制元素在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序中的位置的基础。  
  
   
  
<a name="wcpsdk_layout_amp_introduction"></a>   
## 元素定位简介  
 可以使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 通过多种方式来定位元素。  但是，获得理想的布局不仅要选择正确的 <xref:System.Windows.Controls.Panel> 元素。  需要了解 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>、<xref:System.Windows.FrameworkElement.Margin%2A>、<xref:System.Windows.Controls.Border.Padding%2A> 和 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 属性才能实现精确的定位控制。  
  
 下图显示了一个采用若干定位属性的布局方案。  
  
 ![WPF 定位属性示例](../../../../docs/framework/wpf/advanced/media/layout-margins-padding-alignment-graphic1.png "layout\_margins\_padding\_alignment\_graphic1")  
  
 乍看上去，此图中的 <xref:System.Windows.Controls.Button> 元素可能似乎是随意放置的。  但是，它们的位置实际上是通过使用边距、对齐和空白的组合加以精确控制的。  
  
 下面的示例描述如何创建上图中的布局。  <xref:System.Windows.Controls.Border> 元素封装了父 <xref:System.Windows.Controls.StackPanel>，<xref:System.Windows.Controls.Border.Padding%2A> 值为 15 个[与设备无关的像素](GTMT)。  这就是子 <xref:System.Windows.Controls.StackPanel> 周围会有 <xref:System.Windows.Media.Brushes.LightBlue%2A> 窄带的原因。  <xref:System.Windows.Controls.StackPanel> 的子元素用于举例说明本主题中详细论述的各个不同的定位属性。  将使用三个 <xref:System.Windows.Controls.Button> 元素来演示 <xref:System.Windows.FrameworkElement.Margin%2A> 和 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 属性。  
  
 [!code-csharp[MPALayoutSampleIntro#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutSampleIntro/CSharp/MPA_Layout_Sample_Intro.cs#1)]
 [!code-vb[MPALayoutSampleIntro#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutSampleIntro/VisualBasic/MPALayoutIntro.vb#1)]  
  
 通过下图可以仔细查看前面的示例中使用的各个定位属性。  本主题中后面的各节将更详细地介绍如何使用各个定位属性。  
  
 ![具有屏幕标注的定位属性](../../../../docs/framework/wpf/advanced/media/layout-margins-padding-alignment-graphic2.png "layout\_margins\_padding\_alignment\_graphic2")  
  
<a name="wcpsdk_layout_amp_alignment_properties"></a>   
## 了解 Alignment 属性  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 和 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 属性描述应如何在父元素的已分配布局空间中定位子元素。  通过将这些属性结合使用，您可以精确地定位子元素。  例如，<xref:System.Windows.Controls.DockPanel> 的子元素可以指定四种不同的水平对齐方式：<xref:System.Windows.HorizontalAlignment>、<xref:System.Windows.HorizontalAlignment> 或 <xref:System.Windows.HorizontalAlignment>，或者 <xref:System.Windows.HorizontalAlignment> 以填充可用空间。  类似的值可用于垂直定位。  
  
> [!NOTE]
>  在一个元素上显式设置的 <xref:System.Windows.FrameworkElement.Height%2A> 和 <xref:System.Windows.FrameworkElement.Width%2A> 属性优先于 <xref:System.Windows.HorizontalAlignment> 属性值。  如果尝试设置 <xref:System.Windows.FrameworkElement.Height%2A>, <xref:System.Windows.FrameworkElement.Width%2A> 以及 `Stretch` 的 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 值，将会导致 `Stretch` 请求被忽略。  
  
<a name="wcpsdk_layout_amp_horizontalalignment_properties"></a>   
### HorizontalAlignment 属性  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 属性声明要应用于子元素的水平对齐特性。  下表列出了 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 属性的每个可能的值。  
  
|成员|说明|  
|--------|--------|  
|<xref:System.Windows.HorizontalAlignment>|子元素与父元素的已分配布局空间的左端对齐。|  
|<xref:System.Windows.HorizontalAlignment>|子元素与父元素的已分配布局空间的中心对齐。|  
|<xref:System.Windows.HorizontalAlignment>|子元素与父元素的已分配布局空间的右端对齐。|  
|<xref:System.Windows.HorizontalAlignment>（默认值）|拉伸子元素以填充父元素的已分配布局空间。  显式的 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 值优先。|  
  
 下面的示例演示如何将 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 属性应用于 <xref:System.Windows.Controls.Button> 元素。  将显示每个特性值，以便更好地阐释各种呈现行为。  
  
 [!code-csharp[MPALayoutHorizontalAlignment#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/CSharp/MPA_Layout_HorizontalAlignment.cs#2)]
 [!code-vb[MPALayoutHorizontalAlignment#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/VisualBasic/MPA_Layout_HorizontalAlignment.vb#2)]  
  
 以上代码将产生与下图类似的布局。  在图中可以看到每个 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 值的定位效果。  
  
 ![HorizontalAlignment 示例](../../../../docs/framework/wpf/advanced/media/layout-horizontal-alignment-graphic.png "layout\_horizontal\_alignment\_graphic")  
  
<a name="wcpsdk_layout_amp_verticalalignment_properties"></a>   
### VerticalAlignment 属性  
 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 属性描述要应用于子元素的垂直对齐特性。  下表列出了 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 属性的每个可能的值。  
  
|成员|说明|  
|--------|--------|  
|<xref:System.Windows.VerticalAlignment>|子元素与父元素的已分配布局空间的顶端对齐。|  
|<xref:System.Windows.VerticalAlignment>|子元素与父元素的已分配布局空间的中心对齐。|  
|<xref:System.Windows.VerticalAlignment>|子元素与父元素的已分配布局空间的底端对齐。|  
|<xref:System.Windows.VerticalAlignment>（默认值）|拉伸子元素以填充父元素的已分配布局空间。  显式的 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 值优先。|  
  
 下面的示例演示如何将 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 属性应用于 <xref:System.Windows.Controls.Button> 元素。  将显示每个特性值，以便更好地阐释各种呈现行为。  在此示例中，将使用带有可见网格线的 <xref:System.Windows.Controls.Grid> 元素作为父项，以便更好地阐释各个属性值的布局行为。  
  
 [!code-csharp[MPALayoutVerticalAlignment#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutVerticalAlignment/CSharp/MPA_Layout_VerticalAlignment.cs#2)]
 [!code-vb[MPALayoutVerticalAlignment#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutVerticalAlignment/VisualBasic/MPA_Layout_VerticalAlignment.vb#2)]
 [!code-xml[MPALayoutVerticalAlignment#2](../../../../samples/snippets/xaml/VS_Snippets_Wpf/MPALayoutVerticalAlignment/XAML/default.xaml#2)]  
  
 以上代码将产生与下图类似的布局。  在图中可以看到每个 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 值的定位效果。  
  
 ![VerticalAlignment 属性示例](../../../../docs/framework/wpf/advanced/media/layout-vertical-alignment-graphic.png "layout\_vertical\_alignment\_graphic")  
  
<a name="wcpsdk_layout_amp_margin_properties"></a>   
## 了解 Margin 属性  
 <xref:System.Windows.FrameworkElement.Margin%2A> 属性描述元素与其子级或同级之间的距离。  可通过使用 `Margin="20"` 这样的语法使 <xref:System.Windows.FrameworkElement.Margin%2A> 值统一。  利用此语法，将向元素应用 20 个[与设备无关的像素](GTMT)的统一 <xref:System.Windows.FrameworkElement.Margin%2A>。  <xref:System.Windows.FrameworkElement.Margin%2A> 值也可以采用四个不同值的形式，每个值描述应用于左端、顶端、右端和底端（按该顺序应用）的不同边距，比如 `Margin="0,10,5,25"`。  通过恰当地使用 <xref:System.Windows.FrameworkElement.Margin%2A> 属性，将可以非常精确地控制元素的呈现位置，以及元素的邻近元素和子项的呈现位置。  
  
> [!NOTE]
>  非零的边距会在元素的 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 和 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 外部产生空白。  
  
 下面的示例演示如何在一组 <xref:System.Windows.Controls.Button> 元素的周围应用统一的边距。  <xref:System.Windows.Controls.Button> 元素各个方向的间距都相同，并带有 10 像素的边距缓冲区。  
  
 [!code-cpp[MarginPaddingAlignmentSample#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#1)]
 [!code-csharp[MarginPaddingAlignmentSample#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#1)]
 [!code-vb[MarginPaddingAlignmentSample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#1)]
 [!code-xml[MarginPaddingAlignmentSample#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#1)]  
  
 在许多情况下，统一的边距并不适宜。  对于这些情况，可以应用非统一间距。  下面的示例演示如何将非统一边距间距应用于子元素。  按此顺序描述边距：左端、顶端、右端和底端。  
  
 [!code-cpp[MarginPaddingAlignmentSample#2](../../../../samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#2)]
 [!code-csharp[MarginPaddingAlignmentSample#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#2)]
 [!code-vb[MarginPaddingAlignmentSample#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#2)]
 [!code-xml[MarginPaddingAlignmentSample#2](../../../../samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#2)]  
  
<a name="wcpsdk_layout_amp_padding_properties"></a>   
## 了解 Padding 属性  
 Padding 在大多数方面类似于 <xref:System.Windows.FrameworkElement.Margin%2A>。  Padding 属性只会在少数类上公开，主要是为了方便起见而公开：<xref:System.Windows.Documents.Block>、<xref:System.Windows.Controls.Border>、<xref:System.Windows.Controls.Control> 和 <xref:System.Windows.Controls.TextBlock> 是公开 Padding 属性的类的示例。  <xref:System.Windows.Controls.Border.Padding%2A> 属性可将子元素的有效大小增大指定的 <xref:System.Windows.Thickness> 值。  
  
 下面的示例演示如何将 <xref:System.Windows.Controls.Border.Padding%2A> 应用于父 <xref:System.Windows.Controls.Border> 元素。  
  
 [!code-cpp[MarginPaddingAlignmentSample#3](../../../../samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#3)]
 [!code-csharp[MarginPaddingAlignmentSample#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#3)]
 [!code-vb[MarginPaddingAlignmentSample#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#3)]
 [!code-xml[MarginPaddingAlignmentSample#3](../../../../samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#3)]  
  
<a name="wcpsdk_layout_amp_summary"></a>   
## 在应用程序中使用 Alignment、Margins 和 Padding  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>、<xref:System.Windows.FrameworkElement.Margin%2A>、<xref:System.Windows.Controls.Border.Padding%2A> 和 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 提供了创建复杂的 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 必不可少的定位控制。  您可以利用每个属性的作用来更改子元素定位，从而能够灵活地创建动态的应用程序和用户体验。  
  
 下面的示例演示本主题中详细论述的各个概念。  此示例以本主题第一个示例中的基础结构为基础，添加了一个 <xref:System.Windows.Controls.Grid> 元素作为第一个示例中 <xref:System.Windows.Controls.Border> 的子项。  <xref:System.Windows.Controls.Border.Padding%2A> 应用于父 <xref:System.Windows.Controls.Border> 元素。  <xref:System.Windows.Controls.Grid> 用于划分三个子 <xref:System.Windows.Controls.StackPanel> 元素之间的空间。  将再次使用 <xref:System.Windows.Controls.Button> 元素显示 <xref:System.Windows.FrameworkElement.Margin%2A> 和 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 的不同效果。  将向每个 <xref:System.Windows.Controls.ColumnDefinition> 中添加 <xref:System.Windows.Controls.TextBlock> 元素，以便更好地定义应用于各列中 <xref:System.Windows.Controls.Button> 元素的不同属性。  
  
 [!code-cpp[MarginPaddingAlignmentSample#4](../../../../samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#4)]
 [!code-csharp[MarginPaddingAlignmentSample#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#4)]
 [!code-vb[MarginPaddingAlignmentSample#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#4)]
 [!code-xml[MarginPaddingAlignmentSample#4](../../../../samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#4)]  
  
 编译之后，前面的应用程序将生成类似于下图的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  可以在元素之间的间距中一目了然地看到各个属性值的效果，并且各列中元素的重要属性值显示在 <xref:System.Windows.Controls.TextBlock> 元素内。  
  
 ![一个应用程序中的几个定位属性](../../../../docs/framework/wpf/advanced/media/layout-margins-padding-aligment-graphic3.png "layout\_margins\_padding\_aligment\_graphic3")  
  
<a name="wcpsdk_layout_amp_alignment_whatsnext"></a>   
## 接下来的内容  
 利用 <xref:System.Windows.FrameworkElement> 类定义的定位属性，可以精确地控制元素在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序内的位置。  您现在已了解了多种方法，可以使用这些方法更好地通过 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 来定位元素。  
  
 还提供了一些附加资源，这些资源更加详细地介绍 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局。  [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md) 主题包含有关各个 <xref:System.Windows.Controls.Panel> 元素的更多详细信息。  主题[演练：开始使用 WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)介绍使用布局元素来定位组件并将它们的操作绑定到数据源的高级方法。  
  
## 请参阅  
 <xref:System.Windows.FrameworkElement>   
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>   
 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>   
 <xref:System.Windows.FrameworkElement.Margin%2A>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [布局](../../../../docs/framework/wpf/advanced/layout.md)   
 [WPF Layout Gallery Sample](http://go.microsoft.com/fwlink/?LinkID=160054)