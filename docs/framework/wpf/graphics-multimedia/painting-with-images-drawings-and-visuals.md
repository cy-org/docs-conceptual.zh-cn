---
title: "使用图像、绘图和 Visual 进行绘制 | Microsoft Docs"
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
  - "画笔, 使用绘图进行绘制"
  - "画笔, 使用图像进行绘制"
  - "画笔, 使用可视化效果进行绘制"
  - "使用可视化效果进行绘制"
  - "绘制, 使用绘图"
  - "绘制, 使用图像"
ms.assetid: 779aac3f-8d41-49d8-8130-768244aa2240
caps.latest.revision: 28
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 27
---
# 使用图像、绘图和 Visual 进行绘制
本主题描述如何借助 <xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.DrawingBrush> 和 <xref:System.Windows.Media.VisualBrush> 对象，使用 Image、<xref:System.Windows.Media.Drawing> 或 <xref:System.Windows.Media.Visual> 来绘制区域。  
  
   
  
<a name="prereqs"></a>   
## 必备组件  
 若要了解本主题，您应当熟悉 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供的不同类型的画笔及其基本功能。  有关介绍，请参见 [WPF 画笔概述](../../../../docs/framework/wpf/graphics-multimedia/wpf-brushes-overview.md)。  
  
<a name="image"></a>   
## 使用 Image 绘制区域  
 <xref:System.Windows.Media.ImageBrush> 使用 <xref:System.Windows.Media.ImageSource> 绘制一个区域。  与 <xref:System.Windows.Media.ImageBrush> 一起使用的 <xref:System.Windows.Media.ImageSource> 的最常见类型是 <xref:System.Windows.Media.Imaging.BitmapImage>，它描述一个位图图形。  使用 <xref:System.Windows.Media.Drawing> 对象时，您可以使用 <xref:System.Windows.Media.DrawingImage> 进行绘制，但是使用 <xref:System.Windows.Media.DrawingBrush> 会更简单。  有关 <xref:System.Windows.Media.ImageSource> 对象的更多信息，请参见[图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)。  
  
 若要使用 <xref:System.Windows.Media.ImageBrush> 进行绘制，请创建一个 <xref:System.Windows.Media.Imaging.BitmapImage> 并用它来加载位图内容。  然后，使用 <xref:System.Windows.Media.Imaging.BitmapImage> 来设置 <xref:System.Windows.Media.ImageBrush> 的 <xref:System.Windows.Media.ImageBrush.ImageSource%2A> 属性。  最后，将 <xref:System.Windows.Media.ImageBrush> 应用到想要绘制的对象。  在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中，还可以将 <xref:System.Windows.Media.ImageBrush> 的 <xref:System.Windows.Media.ImageBrush.ImageSource%2A> 属性仅设置为要加载的图像的路径。  
  
 与所有 <xref:System.Windows.Media.Brush> 对象一样，<xref:System.Windows.Media.ImageBrush> 可用于绘制诸如形状、面板、控件和文本之类的对象。  下图显示了利用 <xref:System.Windows.Media.ImageBrush> 可以实现的几种效果。  
  
 ![ImageBrush 输出示例](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-mmgraphics-imagebrushexamples.png "wcpsdk\_mmgraphics\_imagebrushexamples")  
使用 ImageBrush 绘制的对象  
  
 默认情况下，<xref:System.Windows.Media.ImageBrush> 会将其图像拉伸以完全充满要绘制的区域，如果绘制的区域和该图像的长宽比不同，则可能会扭曲该图像。  您可以通过将 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性从默认值 <xref:System.Windows.Media.Stretch> 更改为 <xref:System.Windows.Media.Stretch>、<xref:System.Windows.Media.Stretch> 或 <xref:System.Windows.Media.Stretch> 来更改此行为。  由于 <xref:System.Windows.Media.ImageBrush> 是 <xref:System.Windows.Media.TileBrush> 的一种类型，因此您可以准确指定图像画笔如何填充输出区域，甚至创建图案。  有关 <xref:System.Windows.Media.TileBrush> 高级功能的更多信息，请参见 [TileBrush 概述](../../../../docs/framework/wpf/graphics-multimedia/tilebrush-overview.md)。  
  
<a name="fillingpanelwithimage"></a>   
## 示例：使用位图图像绘制对象  
 以下示例使用 <xref:System.Windows.Media.ImageBrush> 绘制 <xref:System.Windows.Controls.Canvas> 的 <xref:System.Windows.Controls.Panel.Background%2A>。  
  
 [!code-xml[BrushOverviewExamples_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/ImageBrushExample.xaml#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/ImageBrushExample.cs#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/imagebrushexample.vb#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]  
  
<a name="drawingbrushintro"></a>   
## 使用 Drawing 绘制区域  
 可以使用 <xref:System.Windows.Media.DrawingBrush> 来绘制具有形状、文本、图像和视频的区域。  绘图画笔内的形状可能本身就是使用纯色、渐变、图像甚至其他 <xref:System.Windows.Media.DrawingBrush> 绘制而成的。  下图演示了 <xref:System.Windows.Media.DrawingBrush> 的一些用法。  
  
 ![DrawingBrush 输出示例](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-mmgraphics-drawingbrushexamples.png "wcpsdk\_mmgraphics\_drawingbrushexamples")  
使用 DrawingBrush 绘制的对象  
  
 <xref:System.Windows.Media.DrawingBrush> 使用 <xref:System.Windows.Media.Drawing> 对象绘制区域。  <xref:System.Windows.Media.Drawing> 对象描述一些可见内容，例如形状、位图、视频或一行文本。  不同类型的 Drawing 描绘的是不同类型的内容。  下面列出了不同类型的 Drawing 对象。  
  
-   <xref:System.Windows.Media.GeometryDrawing> – 绘制形状。  
  
-   <xref:System.Windows.Media.ImageDrawing> – 绘制图像。  
  
-   <xref:System.Windows.Media.GlyphRunDrawing> – 绘制文本。  
  
-   <xref:System.Windows.Media.VideoDrawing> – 播放音频或视频文件。  
  
-   <xref:System.Windows.Media.DrawingGroup> – 绘制其他绘图。  使用绘图组可以将其他绘图组合成一个复合绘图。  
  
 有关 <xref:System.Windows.Media.Drawing> 对象的更多信息，请参见[Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)。  
  
 如同 <xref:System.Windows.Media.ImageBrush>，<xref:System.Windows.Media.DrawingBrush> 也会拉伸其 <xref:System.Windows.Media.DrawingBrush.Drawing%2A> 以填充其输出区域。  可以通过更改 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性的默认设置 <xref:System.Windows.Media.Stretch> 来重写此行为。  有关更多信息，请参见 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性。  
  
<a name="fillingareawithdrawingbrushexample"></a>   
## 示例：使用 Drawing 绘制对象  
 下面的示例演示如何使用一个具有三个椭圆的 Drawing 来绘制对象。  <xref:System.Windows.Media.GeometryDrawing> 用于描述这些椭圆。  
  
 [!code-xml[BrushOverviewExamples_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/DrawingBrushExample.xaml#graphicsmmdrawingbrushasbuttonbackgroundexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/DrawingBrushExample.cs#graphicsmmdrawingbrushasbuttonbackgroundexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/drawingbrushexample.vb#graphicsmmdrawingbrushasbuttonbackgroundexample1)]  
  
<a name="visualbrushsection"></a>   
## 使用 Visual 绘制区域  
 <xref:System.Windows.Media.VisualBrush> 在所有画笔中功能最多、最强大，它使用 <xref:System.Windows.Media.Visual> 来绘制一个区域。  <xref:System.Windows.Media.Visual> 是一种低级别的图形类型，用作很多有用的图形组件的上级。  例如，<xref:System.Windows.Window>、<xref:System.Windows.FrameworkElement> 和 <xref:System.Windows.Controls.Control> 类都是 <xref:System.Windows.Media.Visual> 对象的类型。  如果使用 <xref:System.Windows.Media.VisualBrush>，则可以使用几乎所有的 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 图形对象来绘制区域。  
  
> [!NOTE]
>  尽管 <xref:System.Windows.Media.VisualBrush> 是一种 <xref:System.Windows.Freezable> 对象，但是当其 <xref:System.Windows.Media.VisualBrush.Visual%2A> 属性设置为非 `null` 的值时，无法将其冻结（设置为只读）。  
  
 指定 <xref:System.Windows.Media.VisualBrush> 的 <xref:System.Windows.Media.VisualBrush.Visual%2A> 内容有两种方法。  
  
-   创建一个新 <xref:System.Windows.Media.Visual>，并使用它来设置 <xref:System.Windows.Media.VisualBrush> 的 <xref:System.Windows.Media.VisualBrush.Visual%2A> 属性。  有关示例，请参见下面的[示例：使用 Visual 绘制对象](#examplevisualbrush1)一节。  
  
-   使用现有 <xref:System.Windows.Media.Visual>，这会创建目标 <xref:System.Windows.Media.Visual> 的重复图像。  然后可以使用 <xref:System.Windows.Media.VisualBrush> 来创建一些有趣的效果，例如反射和放大。  有关示例，请参见[示例：创建反射](#examplevisualbrush2)一节。  
  
 如果您为 <xref:System.Windows.Media.VisualBrush> 定义了一个新的 <xref:System.Windows.Media.VisualBrush.Visual%2A>，并且该 <xref:System.Windows.Media.Visual> 是一个 <xref:System.Windows.UIElement> （例如面板或控件），则当 <xref:System.Windows.Media.VisualBrush.AutoLayoutContent%2A> 属性设置为 `true` 时，布局系统在 <xref:System.Windows.UIElement> 及其子元素上运行。  不过，此根 <xref:System.Windows.UIElement> 实际上是与系统的其余部分隔离的，样式和外部布局无法充满此边界。  因此，应该显式指定该根 <xref:System.Windows.UIElement> 的大小，这是因为其唯一父级是 <xref:System.Windows.Media.VisualBrush>，所以自己无法自动调整大小以适合要绘制的区域。  有关 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中布局的更多信息，请参见[布局](../../../../docs/framework/wpf/advanced/layout.md)。  
  
 如同 <xref:System.Windows.Media.ImageBrush> 和 <xref:System.Windows.Media.DrawingBrush>，<xref:System.Windows.Media.VisualBrush> 也会拉伸其内容以填充其输出区域。  可以通过更改 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性的默认设置 <xref:System.Windows.Media.Stretch> 来重写此行为。  有关更多信息，请参见 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性。  
  
<a name="examplevisualbrush1"></a>   
## 示例：使用 Visual 绘制对象  
 在下面的示例中，将使用几个控件和一个面板来绘制一个矩形。  
  
 [!code-xml[BrushOverviewExamples_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/VisualBrushExample.xaml#graphicsmmvisualbrushasrectanglebackgroundexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/VisualBrushExample.cs#graphicsmmvisualbrushasrectanglebackgroundexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/visualbrushexample.vb#graphicsmmvisualbrushasrectanglebackgroundexample1)]  
  
<a name="examplevisualbrush2"></a>   
## 示例：创建反射  
 上面的示例演示如何新建一个 <xref:System.Windows.Media.Visual> 来用作背景。  您还可以使用 <xref:System.Windows.Media.VisualBrush> 显示现有可视效果；您可以使用此功能生成有趣的视觉效果，例如反射和放大。  下面的示例使用 <xref:System.Windows.Media.VisualBrush> 创建包含若干元素的 <xref:System.Windows.Controls.Border> 的反射。  下面的插图演示此示例生成的输出。  
  
 ![反射的 Visual 对象](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-visualbrush-reflection-small.png "graphicsmm\_visualbrush\_reflection\_small")  
反射的 Visual 对象  
  
 [!code-csharp[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/ReflectionExample.cs#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-vb[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/reflectionexample.vb#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-xml[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/ReflectionExample.xaml#graphicsmmvisualbrushreflectionexamplewholepage)]  
  
 有关演示如何放大屏幕的各部分以及如何创建反射的其他示例，请参见 [VisualBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160049)（VisualBrush 示例）。  
  
<a name="tilebrush"></a>   
## TileBrush 功能  
 <xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.DrawingBrush> 和 <xref:System.Windows.Media.VisualBrush> 都是 <xref:System.Windows.Media.TileBrush> 对象的类型。  通过 <xref:System.Windows.Media.TileBrush> 对象，可以非常自如地控制如何使用图像、绘图或可视元素来绘制区域。  例如，在绘制一个区域时，您可以使用一系列的图像图块创建图案，而不是仅使用拉伸的图像。  
  
 <xref:System.Windows.Media.TileBrush> 包括三个主要的组件：内容、图块和输出区域。  
  
 ![TileBrush 组件](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-mmgraphics-defaultcontentprojection2.png "wcpsdk\_mmgraphics\_defaultcontentprojection2")  
具有单个图块的 TileBrush 的各组成部分  
  
 ![平铺 TileBrush 的组成部分](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-tiledprojection.png "graphicsmm\_tiledprojection")  
具有多个图块的 TileBrush 的各组成部分  
  
 有关 <xref:System.Windows.Media.TileBrush> 对象的图块平铺功能的更多信息，请参见 [TileBrush 概述](../../../../docs/framework/wpf/graphics-multimedia/tilebrush-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.ImageBrush>   
 <xref:System.Windows.Media.DrawingBrush>   
 <xref:System.Windows.Media.VisualBrush>   
 <xref:System.Windows.Media.TileBrush>   
 [TileBrush 概述](../../../../docs/framework/wpf/graphics-multimedia/tilebrush-overview.md)   
 [WPF 画笔概述](../../../../docs/framework/wpf/graphics-multimedia/wpf-brushes-overview.md)   
 [图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [不透明遮罩概述](../../../../docs/framework/wpf/graphics-multimedia/opacity-masks-overview.md)   
 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)   
 [ImageBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160005)   
 [VisualBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160049)