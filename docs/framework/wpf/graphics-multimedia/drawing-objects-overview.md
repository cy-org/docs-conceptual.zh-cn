---
title: "Drawing 对象概述 | Microsoft Docs"
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
  - "Drawing 对象"
  - "DrawingGroup 对象"
  - "绘图, 关于绘图"
  - "GeometryDrawing 对象"
  - "GlyphRunDrawing 对象"
  - "ImageDrawing 对象"
ms.assetid: 9b5ce5c0-e204-4320-a7a8-0b2210d62f88
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Drawing 对象概述
本主题介绍 <xref:System.Windows.Media.Drawing> 对象，并说明如何使用它们来有效地绘制形状、位图、文本和媒体。  创建剪贴画、使用 <xref:System.Windows.Media.DrawingBrush> 绘图或者使用 <xref:System.Windows.Media.Visual> 对象时，可以使用 <xref:System.Windows.Media.Drawing> 对象。  
  
   
  
<a name="whatisadrawingsection"></a>   
## 什么是 Drawing 对象？  
 <xref:System.Windows.Media.Drawing> 对象描述一些可见内容，例如形状、位图、视频或一行文本。  不同类型的 Drawing 描绘的是不同类型的内容。  下面列出了不同类型的 Drawing 对象。  
  
-   <xref:System.Windows.Media.GeometryDrawing> – 绘制形状。  
  
-   <xref:System.Windows.Media.ImageDrawing> – 绘制图像。  
  
-   <xref:System.Windows.Media.GlyphRunDrawing> – 绘制文本。  
  
-   <xref:System.Windows.Media.VideoDrawing> – 播放音频或视频文件。  
  
-   <xref:System.Windows.Media.DrawingGroup> – 绘制其他绘图。  使用绘图组可以将其他绘图组合成一个复合绘图。  
  
 <xref:System.Windows.Media.Drawing> 是一个通用对象；您可以通过多种方式使用 <xref:System.Windows.Media.Drawing> 对象。  
  
-   您可以使用 <xref:System.Windows.Media.DrawingImage> 和 <xref:System.Windows.Controls.Image> 控件将其显示为图像。  
  
-   您可以将其与 <xref:System.Windows.Media.DrawingBrush> 一起使用以绘制对象，例如 <xref:System.Windows.Controls.Page> 的 <xref:System.Windows.Controls.Page.Background%2A>。  
  
-   您可以将其用于描述 <xref:System.Windows.Media.DrawingVisual> 的外观。  
  
-   您可以将其用于枚举 <xref:System.Windows.Media.Visual> 的内容。  
  
 WPF 提供了其他类型的对象，这些对象能够绘制形状、位图、文本和媒体。  例如，您也可以使用 <xref:System.Windows.Shapes.Shape> 对象绘制形状，<xref:System.Windows.Controls.MediaElement> 控件提供了将视频添加到应用程序中的另一种方式。  那么，什么时候应使用 <xref:System.Windows.Media.Drawing> 对象？  当可以牺牲框架级别功能以获取性能优势或需要 <xref:System.Windows.Freezable> 功能时。  由于 <xref:System.Windows.Media.Drawing> 对象缺少对 [布局](../../../../docs/framework/wpf/advanced/layout.md)、输入和焦点的支持，因此它们具有性能优势，是描述背景、剪贴画以及使用 <xref:System.Windows.Media.Visual> 对象进行低级绘制的理想选择。  
  
 由于 <xref:System.Windows.Media.Drawing> 对象是一种类型为 <xref:System.Windows.Freezable> 的对象，因此它们具有若干特殊功能，其中包括可声明为[资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)、可在多个对象之间共享、可设为只读以提高性能、可进行克隆以及可设为线程安全对象。  有关 <xref:System.Windows.Freezable> 对象提供的不同功能的更多信息，请参见 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
<a name="drawinggeometriessection"></a>   
## 绘制形状  
 您可以使用 <xref:System.Windows.Media.GeometryDrawing> 来绘制形状。  几何绘图的 <xref:System.Windows.Media.GeometryDrawing.Geometry%2A> 属性描述要绘制的形状，其 <xref:System.Windows.Media.GeometryDrawing.Brush%2A> 属性描述形状内部的绘制方式，其 <xref:System.Windows.Media.GeometryDrawing.Pen%2A> 属性描述其轮廓的绘制方式。  
  
 下面的示例使用 <xref:System.Windows.Media.GeometryDrawing> 绘制形状。  该形状由 <xref:System.Windows.Media.GeometryGroup> 和两个 <xref:System.Windows.Media.EllipseGeometry> 对象进行描述。  形状内部使用 <xref:System.Windows.Media.LinearGradientBrush> 进行绘制，其轮廓则使用 <xref:System.Windows.Media.Brushes.Black%2A> <xref:System.Windows.Media.Pen> 进行绘制。  
  
 本示例创建以下 <xref:System.Windows.Media.GeometryDrawing>。  
  
 ![两个椭圆的 GeometryDrawing](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-geodraw.png "graphicsmm\_geodraw")  
GeometryDrawing  
  
 [!code-csharp[DrawingMiscSnippets_snip#GeometryDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GeometryDrawingExample.cs#geometrydrawingexampleinline)]
 [!code-xml[DrawingMiscSnippets_snip#GeometryDrawingExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GeometryDrawingExample.xaml#geometrydrawingexampleinline)]  
  
 有关完整的示例，请参见[创建 GeometryDrawing](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-geometrydrawing.md)。  
  
 使用其他 <xref:System.Windows.Media.Geometry> 类（例如 <xref:System.Windows.Media.PathGeometry>），您可以通过创建曲线和弧线来创建更复杂的形状。  有关 <xref:System.Windows.Media.Geometry> 对象的更多信息，请参见 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)。  
  
 有关不使用 <xref:System.Windows.Media.Drawing> 对象绘制形状的其他方法的更多信息，请参见 [WPF 中的形状和基本绘图概述](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)。  
  
<a name="drawingimagessection"></a>   
## 绘制图像  
 您可以使用 <xref:System.Windows.Media.ImageDrawing> 绘制图像。  <xref:System.Windows.Media.ImageDrawing> 对象的 <xref:System.Windows.Media.ImageDrawing.ImageSource%2A> 属性描述要绘制的图像，其 <xref:System.Windows.Media.ImageDrawing.Rect%2A> 属性定义绘制图像的区域。  
  
 下面的示例将在一个矩形的 \(75,75\) 处绘制一个大小为 100 x 100 [像素](GTMT)的图像。  下面的插图显示在示例中创建的 <xref:System.Windows.Media.ImageDrawing>。  添加了一条灰色边框，以显示 <xref:System.Windows.Media.ImageDrawing> 的边界。  
  
 ![在 &#40;75,75&#41; 处绘制的 100 x 100 ImageDrawing](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-simple-imagedrawing-offset.png "graphicsmm\_simple\_imagedrawing\_offset")  
大小为 100 x 100 的 ImageDrawing  
  
 [!code-csharp[DrawingMiscSnippets_snip#ImageDrawing100by100Inline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/ImageDrawingExample.cs#imagedrawing100by100inline)]
 [!code-xml[DrawingMiscSnippets_snip#ImageDrawing100by100Inline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/ImageDrawingExample.xaml#imagedrawing100by100inline)]  
  
 有关图像的更多信息，请参见[图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)。  
  
<a name="playmedia"></a>   
## 播放媒体（仅限代码）  
  
> [!NOTE]
>  虽然您可以在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中声明 <xref:System.Windows.Media.VideoDrawing>，但是只能使用代码加载并播放其媒体。  若要在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中播放视频，请改用 <xref:System.Windows.Controls.MediaElement>。  
  
 您可以使用 <xref:System.Windows.Media.VideoDrawing> 和 <xref:System.Windows.Media.MediaPlayer> 来播放音频或视频文件。  加载并播放媒体的方法有两种。  第一种方法是使用 <xref:System.Windows.Media.MediaPlayer> 和 <xref:System.Windows.Media.VideoDrawing> 自身，第二种方法是创建您自己的 <xref:System.Windows.Media.MediaTimeline>，并将其与 <xref:System.Windows.Media.MediaPlayer> 和 <xref:System.Windows.Media.VideoDrawing> 一起使用。  
  
> [!NOTE]
>  如果媒体随应用程序一起分发，则不能像图像那样将媒体文件用作项目资源。  在项目文件中，必须将媒体类型改设为 `Content`，并将 `CopyToOutputDirectory` 设置为 `PreserveNewest` 或 `Always`。  
  
 若要在不创建自己的 <xref:System.Windows.Media.MediaTimeline> 的情况下播放媒体，请执行下列步骤。  
  
1.  创建 <xref:System.Windows.Media.MediaPlayer> 对象。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline1)]  
  
2.  使用 <xref:System.Windows.Media.MediaPlayer.Open%2A> 方法加载媒体文件。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline2)]  
  
3.  创建 <xref:System.Windows.Media.VideoDrawing>。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline3)]  
  
4.  通过设置 <xref:System.Windows.Media.VideoDrawing> 的 <xref:System.Windows.Media.VideoDrawing.Rect%2A> 属性指定要绘制媒体的大小和位置。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline4)]  
  
5.  使用您创建的 <xref:System.Windows.Media.MediaPlayer> 来设置 <xref:System.Windows.Media.VideoDrawing> 的 <xref:System.Windows.Media.VideoDrawing.Player%2A> 属性。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline5)]  
  
6.  使用 <xref:System.Windows.Media.MediaPlayer> 的 <xref:System.Windows.Media.MediaPlayer.Play%2A> 方法开始播放媒体。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline6)]  
  
 下面的示例使用 <xref:System.Windows.Media.VideoDrawing> 和 <xref:System.Windows.Media.MediaPlayer> 播放视频文件一次。  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 若要对媒体进行更多的计时控制，请将 <xref:System.Windows.Media.MediaTimeline> 与 <xref:System.Windows.Media.MediaPlayer> 和 <xref:System.Windows.Media.VideoDrawing> 对象一起使用。  通过 <xref:System.Windows.Media.MediaTimeline>，您可以指定是否重复播放视频。  若要将 <xref:System.Windows.Media.MediaTimeline> 与 <xref:System.Windows.Media.VideoDrawing> 一起使用，请执行下列步骤：  
  
1.  声明 <xref:System.Windows.Media.MediaTimeline> 并设置其计时行为。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline1)]  
  
2.  从 <xref:System.Windows.Media.MediaTimeline> 创建 <xref:System.Windows.Media.MediaClock>。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline2)]  
  
3.  创建一个 <xref:System.Windows.Media.MediaPlayer> 并使用 <xref:System.Windows.Media.MediaClock> 设置其 <xref:System.Windows.Media.MediaPlayer.Clock%2A> 属性。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline3)]  
  
4.  创建一个 <xref:System.Windows.Media.VideoDrawing>，并将 <xref:System.Windows.Media.MediaPlayer> 分配给 <xref:System.Windows.Media.VideoDrawing> 的 <xref:System.Windows.Media.VideoDrawing.Player%2A> 属性。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline4)]  
  
 下面的示例同时使用 <xref:System.Windows.Media.MediaTimeline> 以及 <xref:System.Windows.Media.MediaPlayer> 和 <xref:System.Windows.Media.VideoDrawing> 来反复播放某视频。  
  
 [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline)]  
  
 请注意，使用 <xref:System.Windows.Media.MediaTimeline> 时，使用从 <xref:System.Windows.Media.MediaClock> 的 <xref:System.Windows.Media.Animation.Clock.Controller%2A> 属性返回的交互式 <xref:System.Windows.Media.Animation.ClockController> 控制媒体播放，而不是使用 <xref:System.Windows.Media.MediaPlayer> 的交互式方法。  
  
<a name="drawtext"></a>   
## 绘制文本  
 您可以使用 <xref:System.Windows.Media.GlyphRunDrawing> 和 <xref:System.Windows.Media.GlyphRun> 来绘制文本。  下面的示例使用 <xref:System.Windows.Media.GlyphRunDrawing> 来绘制文本“Hello World”。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GlyphRunDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GlyphRunDrawingExample.cs#glyphrundrawingexampleinline)]
 [!code-xml[DrawingMiscSnippets_snip#GlyphRunDrawingExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GlyphRunExample.xaml#glyphrundrawingexampleinline)]  
  
 <xref:System.Windows.Media.GlyphRun> 是低级别的对象，拟用于固定格式的文档表示和打印方案。  将文本绘制到屏幕上的一种比较简单的方法是使用 <xref:System.Windows.Controls.Label> 或 <xref:System.Windows.Controls.TextBlock>。  有关 <xref:System.Windows.Media.GlyphRun> 的更多信息，请参见 [GlyphRun 对象和 Glyphs 元素简介](../../../../docs/framework/wpf/advanced/introduction-to-the-glyphrun-object-and-glyphs-element.md)概述。  
  
<a name="compositedrawingssection"></a>   
## 复合绘图  
 使用 <xref:System.Windows.Media.DrawingGroup>，可将多个绘图组合为一个复合绘图。  使用 <xref:System.Windows.Media.DrawingGroup>，您可将形状、图像和文本组合到一个 <xref:System.Windows.Media.Drawing> 对象中。  
  
 下面的示例使用 <xref:System.Windows.Media.DrawingGroup> 将两个 <xref:System.Windows.Media.GeometryDrawing> 对象和一个 <xref:System.Windows.Media.ImageDrawing> 对象组合到一起。  该示例产生下面的输出。  
  
 ![具有多个绘图的 DrawingGroup](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-simple.png "graphicsmm\_simple")  
复合绘图  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmsimpledrawinggroupexample)]
 [!code-xml[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmsimpledrawinggroupexample)]  
  
 通过 <xref:System.Windows.Media.DrawingGroup>，您还可以对其内容应用不透明度蒙版、变换、位图效果及其他操作。  <xref:System.Windows.Media.DrawingGroup> 操作按下列顺序应用：<xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>、<xref:System.Windows.Media.DrawingGroup.Opacity%2A>、<xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>、<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>、<xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A> 和 <xref:System.Windows.Media.DrawingGroup.Transform%2A>。  
  
 下图演示 <xref:System.Windows.Media.DrawingGroup> 操作的应用顺序。  
  
 ![DrawingGroup 操作顺序](../../../../docs/framework/wpf/graphics-multimedia/media/graphcismm-drawinggroup-order.png "graphcismm\_drawinggroup\_order")  
DrawingGroup 操作的顺序  
  
 下表描述您可用于操作 <xref:System.Windows.Media.DrawingGroup> 对象内容的属性。  
  
|属性|说明|图示|  
|--------|--------|--------|  
|<xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>|改变 <xref:System.Windows.Media.DrawingGroup> 内容选定部分的不透明度。  有关示例，请参见[How to: Control the Opacity of a Drawing](http://msdn.microsoft.com/zh-cn/68580652-7d32-4d27-93cc-a5148cf4d5ee)。||  
|<xref:System.Windows.Media.DrawingGroup.Opacity%2A>|统一更改 <xref:System.Windows.Media.DrawingGroup> 内容的不透明度。  使用此属性将 <xref:System.Windows.Media.Drawing> 设置为透明或部分透明。  有关示例，请参见[How to: Apply an Opacity Mask to a Drawing](http://msdn.microsoft.com/zh-cn/d77b420b-9be2-479c-a45e-82f4da30eb9f)。||  
|<xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>|将 <xref:System.Windows.Media.Effects.BitmapEffect> 应用到 <xref:System.Windows.Media.DrawingGroup> 内容。  有关示例，请参见[How to: Apply a BitmapEffect to a Drawing](http://msdn.microsoft.com/zh-cn/c5b1de83-8d09-47fb-96db-5f174471f4b5)。||  
|<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>|将 <xref:System.Windows.Media.DrawingGroup> 内容剪裁到您使用 <xref:System.Windows.Media.Geometry> 描述的区域内。  有关示例，请参见[How to: Clip a Drawing](http://msdn.microsoft.com/zh-cn/1f7d8a2c-c3c2-42cb-a542-e6796f9fb058)。||  
|<xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>|根据指定的准则将[与设备无关的像素](GTMT)与设备像素对齐。  此属性有助于确保清晰地在 DPI 较低的显示器上呈现图形的细节。  有关示例，请参见[向绘图应用 GuidelineSet](../../../../docs/framework/wpf/graphics-multimedia/how-to-apply-a-guidelineset-to-a-drawing.md)。||  
|<xref:System.Windows.Media.DrawingGroup.Transform%2A>|变换 <xref:System.Windows.Media.DrawingGroup> 内容。  有关示例，请参见[How to: Apply a Transform to a Drawing](http://msdn.microsoft.com/zh-cn/0d525f2b-682d-4d67-9660-cf46929fbabd)。||  
  
<a name="usingimagedrawing"></a>   
## 将绘图显示为图像  
 若要使用 <xref:System.Windows.Controls.Image> 控件来显示 <xref:System.Windows.Media.Drawing>，请将 <xref:System.Windows.Media.DrawingImage> 用作 <xref:System.Windows.Controls.Image> 控件的 <xref:System.Windows.Controls.Image.Source%2A>，并将 <xref:System.Windows.Media.DrawingImage> 对象的 <xref:System.Windows.Media.DrawingImage.Drawing%2A?displayProperty=fullName> 属性设置为要显示的绘图。  
  
 下面的示例使用 <xref:System.Windows.Media.DrawingImage> 和 <xref:System.Windows.Controls.Image> 控件显示 <xref:System.Windows.Media.GeometryDrawing>。  该示例产生下面的输出。  
  
 ![两个椭圆的 GeometryDrawing](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-geodraw.png "graphicsmm\_geodraw")  
DrawingImage  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingImageExample.cs#drawingimageexamplewholepage)]
 [!code-xml[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingImageExample.xaml#drawingimageexamplewholepage)]  
  
<a name="renderingwithdrawingbrushsection"></a>   
## 使用 Drawing 绘制对象  
 <xref:System.Windows.Media.DrawingBrush> 是一种使用 Drawing 对象绘制区域的画笔。  您可以使用它来借助 Drawing 绘制任何图形对象。  <xref:System.Windows.Media.DrawingBrush> 的 <xref:System.Windows.Media.Drawing> 属性描述其 <xref:System.Windows.Media.DrawingBrush.Drawing%2A>。  若要使用 <xref:System.Windows.Media.DrawingBrush> 呈现 <xref:System.Windows.Media.Drawing>，请使用画笔的 <xref:System.Windows.Media.Drawing> 属性将其添加到画笔中，并使用画笔绘制图形对象，例如控件或面板。  
  
 下面的示例使用从 <xref:System.Windows.Media.GeometryDrawing> 创建的图案通过 <xref:System.Windows.Media.DrawingBrush> 来绘制 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Shapes.Shape.Fill%2A>。  该示例产生下面的输出。  
  
 ![平铺的 DrawingBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-drawingbrush-geometrydrawing.png "graphicsmm\_drawingbrush\_geometrydrawing")  
与 DrawingBrush 一起使用的 GeometryDrawing  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingBrushExample.cs#drawingbrushexamplewholepage)]
 [!code-xml[DrawingMiscSnippets_snip#DrawingBrushExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingBrushExample.xaml#drawingbrushexamplewholepage)]  
  
 <xref:System.Windows.Media.DrawingBrush> 类提供了用于拉伸和平铺其内容的各种选项。  有关 <xref:System.Windows.Media.DrawingBrush> 的更多信息，请参见[使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)概述。  
  
<a name="renderingwithvisualsection"></a>   
## 使用 Visual 呈现绘图  
 <xref:System.Windows.Media.DrawingVisual> 是一个用于呈现绘图的可视对象类型。  开发人员可以选择直接在可视化层中工作，以生成一个高度自定义的图形环境，本概述中未对此进行说明。  有关更多信息，请参见[使用 DrawingVisual 对象](../../../../docs/framework/wpf/graphics-multimedia/using-drawingvisual-objects.md)概述。  
  
<a name="drawingcontextobjects"></a>   
## DrawingContext 对象  
 通过 <xref:System.Windows.Media.DrawingContext> 类，您可以使用可视化内容填充 <xref:System.Windows.Media.Visual> 或 <xref:System.Windows.Media.Drawing>。  许多此类的低级图形对象使用 <xref:System.Windows.Media.DrawingContext>，因为它能十分有效地描述图形内容。  
  
 虽然 <xref:System.Windows.Media.DrawingContext> 绘图方法看上去与 <xref:System.Drawing.Graphics?displayProperty=fullName> 类型的绘图方法类似，但它们的功能却大相径庭。  <xref:System.Windows.Media.DrawingContext> 用于保留模式图形系统，而 <xref:System.Drawing.Graphics?displayProperty=fullName> 类型则用于即时模式图形系统。  使用 <xref:System.Windows.Media.DrawingContext> 对象的绘图命令时，实际上是在存储一系列呈现指令（但具体的存储机制则取决于提供 <xref:System.Windows.Media.DrawingContext> 的对象的类型）以供图形系统在以后使用，而不是实时绘制到屏幕上。  有关 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 图形系统工作方式的更多信息，请参见 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)。  
  
 绝不能直接实例化 <xref:System.Windows.Media.DrawingContext>；但可以通过某些方法（例如 <xref:System.Windows.Media.DrawingGroup.Open%2A?displayProperty=fullName> 和 <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A?displayProperty=fullName>）获取绘图上下文。  
  
<a name="enumeratevisualcontents"></a>   
## 枚举可视化对象的内容  
 此外，<xref:System.Windows.Media.Drawing> 对象还可提供用来枚举 <xref:System.Windows.Media.Visual> 内容的对象模型。  
  
 下面的示例使用 <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> 方法来检索 <xref:System.Windows.Media.Visual> 的 <xref:System.Windows.Media.DrawingGroup> 值并枚举该值。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
## 请参阅  
 <xref:System.Windows.Media.Drawing>   
 <xref:System.Windows.Media.DrawingGroup>   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [WPF 中的形状和基本绘图概述](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)   
 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)   
 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/drawings-how-to-topics.md)