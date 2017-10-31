---
title: "WPF 画笔概述 | Microsoft Docs"
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
  - "画笔, 关于画笔"
ms.assetid: ecea1955-420b-45c6-bf43-c1404c072c41
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# WPF 画笔概述
屏幕上的所有可见内容之所以可见，是因为它们是由画笔绘制的。  例如，可以使用画笔来描述按钮的背景、文本的前景和形状的填充内容。  本主题介绍了使用 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 画笔进行绘制的概念并提供了示例。  使用画笔，您可以利用任意内容（从简单的纯色到复杂的图案和图像集）绘制[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 对象。  
  
<a name="paintingwithbrush"></a>   
## 使用画笔进行绘制  
 <xref:System.Windows.Media.Brush> 使用其输出对区域进行“绘制”。  画笔不同，其输出类型也不同。  某些画笔使用纯色绘制区域，其他画笔则使用渐变、图案、图像或绘图绘制区域。  下图显示了每个不同 <xref:System.Windows.Media.Brush> 类型的示例。  
  
 ![画笔类型](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brushtypes.png "graphicsmm\_brushtypes")  
画笔示例  
  
 大多数可见对象允许您指定对其进行绘制的方式。  下表列出了一些常见对象和属性，可以对这些对象和属性使用 <xref:System.Windows.Media.Brush>。  
  
|类|画笔属性|  
|-------|----------|  
|<xref:System.Windows.Controls.Border>|<xref:System.Windows.Controls.Border.BorderBrush%2A>, <xref:System.Windows.Controls.Border.Background%2A>|  
|<xref:System.Windows.Controls.Control>|<xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.Foreground%2A>|  
|<xref:System.Windows.Controls.Panel>|<xref:System.Windows.Controls.Panel.Background%2A>|  
|<xref:System.Windows.Media.Pen>|<xref:System.Windows.Media.Pen.Brush%2A>|  
|<xref:System.Windows.Shapes.Shape>|<xref:System.Windows.Shapes.Shape.Fill%2A>, <xref:System.Windows.Shapes.Shape.Stroke%2A>|  
|<xref:System.Windows.Controls.TextBlock>|<xref:System.Windows.Controls.TextBlock.Background%2A>|  
  
 下面部分描述了不同的 <xref:System.Windows.Media.Brush> 类型并提供每个类型的示例。  
  
<a name="paintwithsolidcolorbrush"></a>   
## 使用纯色进行绘制  
 <xref:System.Windows.Media.SolidColorBrush> 使用纯 <xref:System.Windows.Media.Color> 绘制区域。  指定 <xref:System.Windows.Media.SolidColorBrush> 的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 有多种方法：例如，可以指定其 alpha、红色和绿色通道或使用一种由 <xref:System.Windows.Media.Colors> 类提供的预定义颜色之一。  
  
 以下示例使用 <xref:System.Windows.Media.SolidColorBrush> 绘制 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Shapes.Shape.Fill%2A>。  下面的插图显示绘制好的矩形。  
  
 ![使用 SolidColorBrush 绘制的矩形](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-solidcolorbrush.png "graphicsmm\_brush\_ovw\_solidcolorbrush")  
使用 SolidColorBrush 绘制的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmsolidcolorbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmsolidcolorbrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmsolidcolorbrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.SolidColorBrush> 类的更多信息，请参见[使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)。  
  
<a name="paintwithlineargradientbrush"></a>   
## 使用线性渐变进行绘制  
 <xref:System.Windows.Media.LinearGradientBrush> 使用线性渐变绘制区域。  线形渐变横跨一条直线（渐变轴）将两种或更多种色彩进行混合。  可以使用 <xref:System.Windows.Media.GradientStop> 对象指定渐变的颜色及其位置。  
  
 以下示例使用 <xref:System.Windows.Media.LinearGradientBrush> 绘制 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Shapes.Shape.Fill%2A>。  下面的插图显示绘制好的矩形。  
  
 ![使用 LinearGradientBrush 绘制的矩形](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-lineargradientbrush.png "graphicsmm\_brush\_ovw\_lineargradientbrush")  
使用 LinearGradientBrush 绘制的图形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmlineargradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmlineargradientbrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmlineargradientbrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.LinearGradientBrush> 类的更多信息，请参见[使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)。  
  
<a name="paintwithradialgradientbrush"></a>   
## 使用径向渐变进行绘制  
 <xref:System.Windows.Media.RadialGradientBrush> 使用径向渐变绘制区域。  径向渐变跨一个圆将两种或更多种色彩进行混合。  与 <xref:System.Windows.Media.LinearGradientBrush> 类一样，可以使用 <xref:System.Windows.Media.GradientStop> 对象来指定渐变的色彩及其位置。  
  
 以下示例使用 <xref:System.Windows.Media.RadialGradientBrush> 绘制 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Shapes.Shape.Fill%2A>。  下面的插图显示绘制好的矩形。  
  
 ![使用 RadialGradientBrush 绘制的矩形](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-radialgradientbrush.png "graphicsmm\_brush\_ovw\_radialgradientbrush")  
使用 RadialGradientBrush 绘制的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmradialgradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmradialgradientbrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmradialgradientbrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.RadialGradientBrush> 类的更多信息，请参见[使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)。  
  
<a name="paintwithimage"></a>   
## 使用图像进行绘制  
 <xref:System.Windows.Media.ImageBrush> 使用 <xref:System.Windows.Media.ImageSource> 绘制一个区域。  
  
 以下示例使用 <xref:System.Windows.Media.ImageBrush> 绘制 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Shapes.Shape.Fill%2A>。  下面的插图显示绘制好的矩形。  
  
 ![使用 ImageBrush 绘制的矩形](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-imagebrush.png "graphicsmm\_brush\_ovw\_imagebrush")  
使用图像绘制的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmimagebrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmimagebrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmimagebrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.ImageBrush> 类的更多信息，请参见[使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)。  
  
<a name="paintwithdrawing"></a>   
## 使用绘图进行绘制  
 <xref:System.Windows.Media.DrawingBrush> 使用 <xref:System.Windows.Media.Drawing> 绘制一个区域。  <xref:System.Windows.Media.Drawing> 可以包含形状、图像、文本和媒体。  
  
 以下示例使用 <xref:System.Windows.Media.DrawingBrush> 绘制 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Shapes.Shape.Fill%2A>。  下面的插图显示绘制好的矩形。  
  
 ![使用 DrawingBrush 绘制的矩形](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-drawingbrush.png "graphicsmm\_brush\_ovw\_drawingbrush")  
使用 DrawingBrush 绘制的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmdrawingbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmdrawingbrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmdrawingbrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.DrawingBrush> 类的更多信息，请参见[使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)。  
  
<a name="paintwithvisual"></a>   
## 使用 Visual 进行绘制  
 <xref:System.Windows.Media.VisualBrush> 使用 <xref:System.Windows.Media.Visual> 对象绘制区域。  Visual 对象的示例包括 <xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.Page> 和 <xref:System.Windows.Controls.MediaElement>。  使用 <xref:System.Windows.Media.VisualBrush> 还可以将内容从应用程序的一个部分提取到另一个区域，在创建反射效果和放大局部屏幕时将会非常有用。  
  
 以下示例使用 <xref:System.Windows.Media.VisualBrush> 绘制 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Shapes.Shape.Fill%2A>。  下面的插图显示绘制好的矩形。  
  
 ![使用 VisualBrush 绘制的矩形](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-visualbrush.png "graphicsmm\_brush\_ovw\_visualbrush")  
使用 VisualBrush 绘制的矩形  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmvisualbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmvisualbrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmvisualbrushexampleinline)]  
  
 有关 <xref:System.Windows.Media.VisualBrush> 类的更多信息，请参见[使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)。  
  
<a name="paintwithpredefinedbrushesandsystemcolors"></a>   
## 使用预定义画笔和系统画笔进行绘制  
 为了方便起见，[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 提供了一组预定义画笔和系统画笔，您可以使用这些画笔来绘制对象。  
  
-   有关可用预定义画笔的列表，请参见 <xref:System.Windows.Media.Brushes> 类。  有关演示如何使用预定义画笔的示例，请参见[使用纯色绘制区域](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-solid-color.md)。  
  
-   有关可用系统画笔的列表，请参见 <xref:System.Windows.SystemColors> 类。  有关示例，请参见[使用系统画笔绘制区域](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)。  
  
<a name="commonbrushfeatures"></a>   
## 常见画笔功能  
 <xref:System.Windows.Media.Brush> 对象提供了 <xref:System.Windows.Media.Brush.Opacity%2A> 属性，可以通过该属性使画笔显示为透明或半透明。  如果 <xref:System.Windows.Media.Brush.Opacity%2A> 的值为 0，则画笔显示完全透明；如果 <xref:System.Windows.Media.Brush.Opacity%2A> 的值为 1，则画笔显示为完全不透明。  下面的示例使用 <xref:System.Windows.Media.Brush.Opacity%2A> 属性使 <xref:System.Windows.Media.SolidColorBrush> 具有 25% 的不透明度。  
  
 [!code-xml[BrushOverviewExamples_snip#OpacityExample1XAML](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/OpacityExample.xaml#opacityexample1xaml)]  
  
 [!code-csharp[BrushOverviewExamples_snip#OpacityExample1CSharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/OpacityExample.cs#opacityexample1csharp)]  
  
 如果画笔包含部分透明的颜色，则通过相乘将该颜色的不透明度的值与画笔的不透明度值进行结合。  例如，如果画笔的不透明度值为 0.5，画笔中使用颜色的不透明度值也是 0.5，则输出颜色的不透明度值为 0.25。  
  
> [!NOTE]
>  与使用元素的 <xref:System.Windows.UIElement.Opacity%2A?displayProperty=fullName> 属性来更改整个元素的不透明度相比，更改画笔的不透明度值将会更有效。  
  
 您可以使用画笔的 <xref:System.Windows.Media.Brush.Transform%2A> 或 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 属性对画笔的内容进行旋转、缩放、扭曲和平移。  有关更多信息，请参见[Brush 变换概述](../../../../docs/framework/wpf/graphics-multimedia/brush-transformation-overview.md)。  
  
 由于它们是 <xref:System.Windows.Media.Animation.Animatable> 的对象，因此也可以对 <xref:System.Windows.Media.Brush> 进行动画处理。  有关更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
<a name="freezable_features"></a>   
### Freezable 功能  
 由于它继承自 <xref:System.Windows.Freezable> 类，因此 <xref:System.Windows.Media.Brush> 类提供了一些特殊功能：<xref:System.Windows.Media.Brush> 对象可声明为[资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)、在多个对象之间共享以及进行克隆。  另外，除 <xref:System.Windows.Media.VisualBrush> 外，所有的 <xref:System.Windows.Media.Brush> 类型都可以设为只读以提高性能和成为线程安全的类型。  
  
 有关 <xref:System.Windows.Freezable> 对象提供的不同功能的更多信息，请参见 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
 有关无法冻结 <xref:System.Windows.Media.VisualBrush> 对象的原因的更多信息，请参见 <xref:System.Windows.Media.VisualBrush> 类型页。  
  
## 请参阅  
 <xref:System.Windows.Media.Brush>   
 <xref:System.Windows.Media.Brushes>   
 [使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [Brushes Sample](http://go.microsoft.com/fwlink/?LinkID=159973)   
 [ImageBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160005)   
 [VisualBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160049)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/brushes-how-to-topics.md)   
 [其他性能建议](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)