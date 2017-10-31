---
title: "优化性能：二维图形和图像处理 | Microsoft Docs"
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
  - "二维图形"
  - "绘图, 优化性能"
  - "图形, 性能"
  - "图像, 优化性能"
  - "图像处理, 优化性能"
  - "形状, 优化性能"
ms.assetid: e335601e-28c8-4d64-ba27-778fffd55f72
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 优化性能：二维图形和图像处理
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了多种二维图形和图像处理功能，可以针对您的应用程序要求优化这些功能。  本主题提供有关二维图形和图像处理性能优化的信息。  
  
   
  
<a name="Drawing_and_Shapes"></a>   
## 绘图和形状  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了 <xref:System.Windows.Media.Drawing> 和 <xref:System.Windows.Shapes.Shape> 这两个对象以表示绘图内容。  不过，<xref:System.Windows.Media.Drawing> 对象比 <xref:System.Windows.Shapes.Shape> 对象结构简单并且性能特性更为优良。  
  
 使用 <xref:System.Windows.Shapes.Shape>，可以在屏幕上绘制图形形状。  由于 <xref:System.Windows.Shapes.Shape> 对象派生于 <xref:System.Windows.FrameworkElement> 类，因此它们可以在面板和大多数控件中使用。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了对图形和呈现服务的若干层访问。  在顶层，<xref:System.Windows.Shapes.Shape> 对象很容易使用，并且提供了许多有用的功能，例如布局和事件处理。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了大量随时可用的形状对象。  所有形状对象都是从 <xref:System.Windows.Shapes.Shape> 类继承的。  可用的形状对象有 <xref:System.Windows.Shapes.Ellipse>、<xref:System.Windows.Shapes.Line>、<xref:System.Windows.Shapes.Path>、<xref:System.Windows.Shapes.Polygon>、<xref:System.Windows.Shapes.Polyline> 和 <xref:System.Windows.Shapes.Rectangle>。  
  
 <xref:System.Windows.Media.Drawing> 对象不是派生自 <xref:System.Windows.FrameworkElement> 类，相比而言它更轻量地实现形状、图像和文本的呈现。  
  
 有以下四种类型的 <xref:System.Windows.Media.Drawing> 对象：  
  
-   <xref:System.Windows.Media.GeometryDrawing>：绘制形状。  
  
-   <xref:System.Windows.Media.ImageDrawing>：绘制图像。  
  
-   <xref:System.Windows.Media.GlyphRunDrawing>：绘制文本。  
  
-   <xref:System.Windows.Media.DrawingGroup>：绘制其他绘图。  使用绘图组可以将其他绘图组合成一个复合绘图。  
  
 <xref:System.Windows.Media.GeometryDrawing> 对象用于呈现几何图形内容。  <xref:System.Windows.Media.Geometry> 类以及从中派生的具体类（如 <xref:System.Windows.Media.CombinedGeometry>、<xref:System.Windows.Media.EllipseGeometry> 和 <xref:System.Windows.Media.PathGeometry>）提供二维图形的呈现方式，此外还提供命中测试和剪辑支持。  例如，Geometry 对象可用于定义控件的区域，或者定义要应用到图像的剪辑区域。  Geometry 对象可以是简单的区域（如矩形和圆形），也可以是基于两个或多个几何图形对象创建的复合区域。  通过组合 <xref:System.Windows.Media.PathSegment> 派生的对象（例如 <xref:System.Windows.Media.ArcSegment>、<xref:System.Windows.Media.BezierSegment> 和 <xref:System.Windows.Media.QuadraticBezierSegment>），可以创建较复杂的几何图形区域。  
  
 从表面上看，<xref:System.Windows.Media.Geometry> 类和 <xref:System.Windows.Shapes.Shape> 类十分相似。  它们都可用来呈现二维图形，并且从其自身派生的具体类也很相似，例如 <xref:System.Windows.Media.EllipseGeometry> 和 <xref:System.Windows.Shapes.Ellipse>。  然而，这两种类之间存在着重大差异。  其中有一个差异就是 <xref:System.Windows.Media.Geometry> 类没有 <xref:System.Windows.Shapes.Shape> 类的某些功能，例如自行绘制的功能。  若要绘制一个几何图形对象，必须使用其他类（例如 DrawingContext、Drawing 或 Path，需要注意 Path 是一种 Shape）来执行此绘制操作。  诸如填充、笔画和笔画粗细之类的呈现属性针对绘制此几何图形对象的类，而形状对象包括这些属性。  可以这样来理解此差异：几何图形对象定义一个区域（如圆形），而形状对象不仅定义一个区域，还定义如何填充和描绘此区域并参与布局系统。  
  
 由于 <xref:System.Windows.Shapes.Shape> 对象派生自 <xref:System.Windows.FrameworkElement> 类，因此使用此对象会大大增加应用程序的内存消耗。  如果事实上您的图形内容无需使用 <xref:System.Windows.FrameworkElement> 功能，则可以考虑使用轻量的 <xref:System.Windows.Media.Drawing> 对象。  
  
 有关 <xref:System.Windows.Media.Drawing> 对象的更多信息，请参见 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)。  
  
<a name="StreamGeometry_Objects"></a>   
## StreamGeometry 对象  
 <xref:System.Windows.Media.StreamGeometry> 对象是 <xref:System.Windows.Media.PathGeometry> 的一个轻量替代品，可用于创建几何形状。  若要描述复杂的几何图形，请使用 <xref:System.Windows.Media.StreamGeometry>。  <xref:System.Windows.Media.StreamGeometry> 是经过优化的，可用于处理多个 <xref:System.Windows.Media.PathGeometry> 对象，并且相对于使用多个独立的 <xref:System.Windows.Media.PathGeometry> 对象而言，其执行效率更高。  
  
 下面的示例使用特性语法用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 创建一个三角形 <xref:System.Windows.Media.StreamGeometry>。  
  
 [!code-xml[GeometriesMiscSnippets_snip#StreamGeometryTriangleExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/StreamGeometryExample.xaml#streamgeometrytriangleexamplewholepage)]  
  
 有关 <xref:System.Windows.Media.StreamGeometry> 对象的更多信息，请参见[使用 StreamGeometry 创建形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-using-a-streamgeometry.md)。  
  
<a name="DrawingVisual_Objects"></a>   
## DrawingVisual 对象  
 <xref:System.Windows.Media.DrawingVisual> 对象是一个用于呈现形状、图像或文本的轻量绘图类。  此类之所以被视为轻量，是因为它不提供布局或事件处理功能，从而能够改善其性能。  因此，绘图最适于背景和剪贴画。  有关更多信息，请参见[使用 DrawingVisual 对象](../../../../docs/framework/wpf/graphics-multimedia/using-drawingvisual-objects.md)。  
  
<a name="Images"></a>   
## 图像  
 与以前版本的 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 中的图像处理功能相比，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 图像处理功能有很大的改进。  图像处理功能（例如在常用控件上显示位图或使用图像）主要由 Microsoft Windows 图形设备接口 \(GDI\) 或 Microsoft Windows GDI\+ 应用程序编程接口 \(API\) 来处理。  这些 API 提供了基线图像处理功能，但缺乏诸如编解码器扩展性支持和高保真图像支持之类的功能。  WPF 图像处理 API 已进行重新设计以克服 GDI 和 GDI\+ 的缺点，并提供一组新的 API 用于在应用程序中显示和使用图像。  
  
 使用图像时，为了获得更好的性能，请考虑下面的建议：  
  
-   如果应用程序要求您显示缩略图像，则考虑创建此图像的小型版本。  默认情况下，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 以完整大小加载图像并进行解码。  如果您只需要缩略版本的图像，则 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 不必将图像解码为其完整大小再缩小至缩略图大小。  为了避免这种不必要的系统开销，您可以请求 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将图像解码为缩略图大小，或者请求 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 加载缩略图大小的图像。  
  
-   始终将图像解码为所需的大小而不是默认的大小。  如上所述，请求 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将图像解码为所需的大小，而不是默认的完整大小。  这样不仅缩小了应用程序的工作集，而且还提高了执行速度。  
  
-   如有可能，可以将多个图像组合成单个图像，例如将多个图像组合成一个幻灯胶片。  
  
-   有关更多信息，请参见[图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)。  
  
### BitmapScalingMode  
 在对任意位图的缩放进行动画处理时，默认的高质量图像重新取样算法有时可能会使用过多的系统资源，引起帧速率降级，并导致动画明显变慢。  通过将 <xref:System.Windows.Media.RenderOptions> 对象的 <xref:System.Windows.Media.RenderOptions.BitmapScalingMode%2A> 属性设置为 <xref:System.Windows.Media.BitmapScalingMode>，可在缩放位图时创建较流畅的动画。  <xref:System.Windows.Media.BitmapScalingMode> 模式通知 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 呈现引擎在处理图像时从质量优化算法切换到速度优化算法。  
  
 下面的示例演示如何设置图像对象的 <xref:System.Windows.Media.BitmapScalingMode>。  
  
 [!code-csharp[RenderOptions#RenderOptionsSnippet2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RenderOptions/CSharp/Window1.xaml.cs#renderoptionssnippet2)]
 [!code-vb[RenderOptions#RenderOptionsSnippet2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RenderOptions/visualbasic/window1.xaml.vb#renderoptionssnippet2)]  
  
### CachingHint  
 默认情况下，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 不缓存 <xref:System.Windows.Media.TileBrush> 对象（例如 <xref:System.Windows.Media.DrawingBrush> 和 <xref:System.Windows.Media.VisualBrush>）的已呈现内容。  在内容或场景中对 <xref:System.Windows.Media.TileBrush> 的使用均不更改的静态情况下，此功能很有用，因为它可以节省视频内存。  在以非静态方式使用具有静态内容的 <xref:System.Windows.Media.TileBrush> 时 – 例如，当静态的 <xref:System.Windows.Media.DrawingBrush> 或 <xref:System.Windows.Media.VisualBrush> 映射到旋转三维对象的表面时，此功能的作用不大。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的默认行为是逐帧重新呈现 <xref:System.Windows.Media.DrawingBrush> 或 <xref:System.Windows.Media.VisualBrush> 的整个内容，即使内容没有更改也是如此。  
  
 通过将 <xref:System.Windows.Media.RenderOptions> 对象的 <xref:System.Windows.Media.RenderOptions.CachingHint%2A> 属性设置为 <xref:System.Windows.Media.CachingHint>，可以使用图块画笔对象的缓存版本来提高性能。  
  
 <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMinimum%2A> 和 <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A> 属性值是相对大小值，可确定由于比例更改而应重新生成 <xref:System.Windows.Media.TileBrush> 对象的时间。  例如，如果将 <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A> 属性设置为 2.0，则仅当 <xref:System.Windows.Media.TileBrush> 的缓存大小超过当前缓存大小的两倍时，才需要重新生成。  
  
 下面的示例演示如何将缓存提示选项用于 <xref:System.Windows.Media.DrawingBrush>。  
  
 [!code-csharp[RenderOptions#RenderOptionsSnippet3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RenderOptions/CSharp/Window1.xaml.cs#renderoptionssnippet3)]
 [!code-vb[RenderOptions#RenderOptionsSnippet3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RenderOptions/visualbasic/window1.xaml.vb#renderoptionssnippet3)]  
  
## 请参阅  
 [优化 WPF 应用程序性能](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [规划应用程序性能](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [利用硬件](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [布局和设计](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [对象行为](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [应用程序资源](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [其他性能建议](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)   
 [动画提示和技巧](../../../../docs/framework/wpf/graphics-multimedia/animation-tips-and-tricks.md)