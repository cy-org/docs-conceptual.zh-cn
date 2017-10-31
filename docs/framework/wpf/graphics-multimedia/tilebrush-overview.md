---
title: "TileBrush 概述 | Microsoft Docs"
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
  - "画笔, TileBrush"
  - "TileBrush"
ms.assetid: aa4a7b7e-d09d-44c2-8d61-310c50e08d68
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# TileBrush 概述
使用 <xref:System.Windows.Media.TileBrush> 对象，您可以非常自如地控制如何使用图像、<xref:System.Windows.Media.Drawing> 或 <xref:System.Windows.Media.Visual> 来绘制区域。  本主题介绍如何使用 <xref:System.Windows.Media.TileBrush> 功能来更自如地控制 <xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.DrawingBrush> 或 <xref:System.Windows.Media.VisualBrush> 绘制区域的方式。  
  
   
  
<a name="prerequisite"></a>   
## 必备组件  
 了解如何使用 <xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.DrawingBrush> 或 <xref:System.Windows.Media.VisualBrush> 类的基本功能对于了解本主题是很有帮助的。  有关这些类型的简介，请参见[使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)。  
  
<a name="tilebrush"></a>   
## 使用图块绘制区域  
 <xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.DrawingBrush> 和 <xref:System.Windows.Media.VisualBrush> 是 <xref:System.Windows.Media.TileBrush> 对象的类型。  使用图块画笔，您可以非常自如地控制如何使用图像、绘图或可视元素来绘制区域。  例如，在绘制一个区域时，您可以使用一系列的图像图块创建图案，而不是仅使用拉伸的图像。  
  
 使用图块画笔绘制区域涉及以下三个组成部分：内容、基本图块和输出区域。  
  
 ![TileBrush 组件](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-mmgraphics-defaultcontentprojection2.png "wcpsdk\_mmgraphics\_defaultcontentprojection2")  
具有单个图块的 TileBrush 的各组成部分  
  
 ![平铺 TileBrush 的组成部分](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-tiledprojection.png "graphicsmm\_tiledprojection")  
指定了图块的 TileMode 的 TileBrush 的各组成部分  
  
 输出区域指绘制的区域，如 <xref:System.Windows.Shapes.Ellipse> 的 <xref:System.Windows.Shapes.Shape.Fill%2A> 或 <xref:System.Windows.Controls.Button> 的 <xref:System.Windows.Controls.Control.Background%2A>。  下面各节介绍了 <xref:System.Windows.Media.TileBrush> 的另外两个组成部分。  
  
<a name="brushcontent"></a>   
## 画笔内容  
 有三种类型的 <xref:System.Windows.Media.TileBrush>，它们分别使用一种不同类型的内容进行绘制。  
  
-   如果画笔为 <xref:System.Windows.Media.ImageBrush>，则此内容为图像。<xref:System.Windows.Media.ImageBrush.ImageSource%2A> 属性指定 <xref:System.Windows.Media.ImageBrush> 的内容。  
  
-   如果画笔为 <xref:System.Windows.Media.DrawingBrush>，则此内容为绘图。  <xref:System.Windows.Media.DrawingBrush.Drawing%2A> 属性指定 <xref:System.Windows.Media.DrawingBrush> 的内容。  
  
-   如果画笔为 <xref:System.Windows.Media.VisualBrush>，则此内容为可视元素。  <xref:System.Windows.Media.VisualBrush.Visual%2A> 属性指定 <xref:System.Windows.Media.VisualBrush> 的内容。  
  
 尽管通常情况下将 <xref:System.Windows.Media.TileBrush.Viewbox%2A> 的设置保留为默认值，但您也可以使用 <xref:System.Windows.Media.TileBrush.Viewbox%2A> 属性来指定 <xref:System.Windows.Media.TileBrush> 内容的位置和尺寸。  默认情况下，<xref:System.Windows.Media.TileBrush.Viewbox%2A> 配置为完全包含画笔的内容。  有关配置 <xref:System.Windows.Controls.Viewbox> 的更多信息，请参见 <xref:System.Windows.Controls.Viewbox> 属性页。  
  
<a name="thebasetile"></a>   
## 基本图块  
 <xref:System.Windows.Media.TileBrush> 将其内容投射到基本图块中。  <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性控制如何拉伸 <xref:System.Windows.Media.TileBrush> 内容来填充基本图块。  <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性接受 <xref:System.Windows.Media.Stretch> 枚举定义的以下值：  
  
-   <xref:System.Windows.Media.Stretch>：不拉伸画笔的内容来填充图块。  
  
-   <xref:System.Windows.Media.Stretch>：缩放画笔的内容以适合图块。  由于内容的高度和宽度是独立缩放的，因此内容的原始长宽比可能不会保留。  也就是说，为了完全填充输出图块，画笔的内容可能会扭曲。  
  
-   <xref:System.Windows.Media.Stretch>：缩放画笔的内容使其完全放置于图块内。  内容的长宽比保留。  
  
-   <xref:System.Windows.Media.Stretch>：缩放画笔的内容，使它完全填充输出区域，同时保留内容的原始长宽比。  
  
 下图举例说明了不同的 <xref:System.Windows.Media.TileBrush.Stretch%2A> 设置。  
  
 ![不同的 TileBrush 拉伸设置](../../../../docs/framework/wpf/graphics-multimedia/media/img-mmgraphics-stretchenum.png "img\_mmgraphics\_stretchenum")  
  
 在下面的示例中，将 <xref:System.Windows.Media.ImageBrush> 的内容设置为不通过拉伸来填充输出区域。  
  
 [!code-xml[BrushOverviewExamples_snip#GraphicsMMNoStretchExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/StretchExample.xaml#graphicsmmnostretchexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMNoStretchExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/StretchExample.cs#graphicsmmnostretchexample)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMNoStretchExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/stretchexample.vb#graphicsmmnostretchexample)]  
  
 默认情况下，<xref:System.Windows.Media.TileBrush> 生成单个图块（基本图块）并拉伸此图块以完全填充输出区域。  您可以通过设置 <xref:System.Windows.Media.TileBrush.Viewport%2A> 和 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 属性来更改基本图块的大小和位置。  
  
<a name="basetilesize"></a>   
### 基本图块大小  
 <xref:System.Windows.Media.TileBrush.Viewport%2A> 属性决定了基本图块的大小和位置，<xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 属性决定了 <xref:System.Windows.Media.TileBrush.Viewport%2A> 是使用绝对坐标还是相对坐标指定的。  如果坐标是相对的，则是相对于输出区域的大小而言。  点 \(0,0\) 表示输出区域的左上角，\(1,1\) 表示输出区域的右下角。  要指定 <xref:System.Windows.Media.TileBrush.Viewport%2A> 属性使用绝对坐标，请将 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 属性设置为 <xref:System.Windows.Media.BrushMappingMode>。  
  
 下图演示了使用相对和绝对 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 的 <xref:System.Windows.Media.TileBrush> 在输出上的差异。  请注意每个图均显示了一种图块图案；下一节介绍如何指定图块图案。  
  
 ![绝对和相对视区单位](../../../../docs/framework/wpf/graphics-multimedia/media/absolute-and-relative-viewports.png "absolute\_and\_relative\_viewports")  
  
 在下面的示例中，使用一幅图像来创建一个宽和高各为 50% 的图块。  基本图块位于输出区域的 \(0,0\)。  
  
 [!code-xml[BrushOverviewExamples_snip#GraphicsMMRelativeViewportUnitsExample1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileSizeExample.xaml#graphicsmmrelativeviewportunitsexample1)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMRelativeViewportUnitsExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/TileSizeExample.cs#graphicsmmrelativeviewportunitsexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMRelativeViewportUnitsExample1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/tilesizeexample.vb#graphicsmmrelativeviewportunitsexample1)]  
  
 下一个示例将 <xref:System.Windows.Media.ImageBrush> 的图块设置为 25 x 25 个[与设备无关的像素](GTMT)。  因为 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 是绝对的，所以 <xref:System.Windows.Media.ImageBrush> 图块总是 25 x 25 像素，而不管绘制区域的大小是多少。  
  
 [!code-xml[BrushOverviewExamples_snip#GraphicsMMAbsoluteViewportUnitsExample1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileSizeExample.xaml#graphicsmmabsoluteviewportunitsexample1)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMAbsoluteViewportUnitsExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/TileSizeExample.cs#graphicsmmabsoluteviewportunitsexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMAbsoluteViewportUnitsExample1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/tilesizeexample.vb#graphicsmmabsoluteviewportunitsexample1)]  
  
<a name="tilingbehavior"></a>   
### 图块平铺行为  
 当基本图块未完全填充输出区域并且指定了 <xref:System.Windows.Media.TileMode> 以外的平铺模式时，<xref:System.Windows.Media.TileBrush> 将生成一种图块图案。  当图块画笔的图块未完全填充输出区域时，其 <xref:System.Windows.Media.TileBrush.TileMode%2A> 属性即指定是否应复制基本图块来填充输出区域，并进一步指定在要复制的情况下如何复制基本图块。  <xref:System.Windows.Media.TileBrush.TileMode%2A> 属性接受 <xref:System.Windows.Media.TileMode> 枚举定义的以下值：  
  
-   <xref:System.Windows.Media.TileMode>：仅绘制基本图块。  
  
-   <xref:System.Windows.Media.TileMode>：绘制基本图块，并通过重复基本图块来填充剩余的区域，使一个图块的右边缘靠近下一个图块的左边缘，底边缘和顶边缘也是如此。  
  
-   <xref:System.Windows.Media.TileMode>：与 <xref:System.Windows.Media.TileMode> 相同，只不过图块的交替列水平翻转。  
  
-   <xref:System.Windows.Media.TileMode>：与 <xref:System.Windows.Media.TileMode> 相同，只不过图块的交替行垂直翻转。  
  
-   <xref:System.Windows.Media.TileMode>：<xref:System.Windows.Media.TileMode> 和 <xref:System.Windows.Media.TileMode> 的组合。  
  
 下图举例说明了不同的图块模式。  
  
 ![不同的 TileBrush TileMode 设置](../../../../docs/framework/wpf/graphics-multimedia/media/img-mmgraphics-tilemodes.png "img\_mmgraphics\_tilemodes")  
  
 在下面的示例中，用一个图像来绘制 100 像素宽、100 像素高的矩形。  通过将画笔的 <xref:System.Windows.Media.TileBrush.Viewport%2A> 设置为 0,0,0.25,0.25，使画笔的基本图块占输出区域的 1\/4。  画笔的 <xref:System.Windows.Media.TileBrush.TileMode%2A> 设置为 <xref:System.Windows.Media.TileMode>。  以使它用图块行来填充矩形。  
  
 [!code-xml[BrushOverviewExamples_snip#GraphicsMMFlipXYExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TilingExample.xaml#graphicsmmflipxyexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMFlipXYExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/TilingExample.cs#graphicsmmflipxyexample)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMFlipXYExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/tilingexample.vb#graphicsmmflipxyexample)]  
  
## 请参阅  
 <xref:System.Windows.Media.ImageBrush>   
 <xref:System.Windows.Media.DrawingBrush>   
 <xref:System.Windows.Media.VisualBrush>   
 <xref:System.Windows.Media.TileBrush>   
 [使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/brushes-how-to-topics.md)   
 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [ImageBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160005)   
 [VisualBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160049)