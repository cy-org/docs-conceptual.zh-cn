---
title: "Geometry 概述 | Microsoft Docs"
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
  - "类, 几何图形"
  - "CombinedGeometry 类"
  - "EllipseGeometry 类"
  - "几何图形类"
  - "图形, 几何图形类"
  - "LineGeometry 类"
  - "PathGeometry 类"
  - "RectangleGeometry 类"
ms.assetid: 9fba8934-98b7-4af6-82f6-f4ef887f963a
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# Geometry 概述
本概述介绍如何使用 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Media.Geometry> 类来描绘形状。  本主题还比较了 <xref:System.Windows.Media.Geometry> 对象与 <xref:System.Windows.Shapes.Shape> 元素之间的区别。  
  
   
  
<a name="wcpsdk_graphics_geometry_introduction"></a>   
## 什么是 Geometry？  
 使用 <xref:System.Windows.Media.Geometry> 类以及派生自它的其他类（如 <xref:System.Windows.Media.EllipseGeometry>、<xref:System.Windows.Media.PathGeometry> 和 <xref:System.Windows.Media.CombinedGeometry>），可以描绘二维形状的几何图形。  这些几何图形的描绘具有许多用途，例如，定义一个要绘制到屏幕的形状或者定义命中测试和剪辑区域。  您甚至可以使用 Geometry 来定义动画路径。  
  
 <xref:System.Windows.Media.Geometry> 对象可以很简单，例如矩形和圆形，也可以是基于两个或更多个 Geometry 对象创建的复合形状。  使用 <xref:System.Windows.Media.PathGeometry> 和 <xref:System.Windows.Media.StreamGeometry> 类可以创建更复杂的几何图形，这两个类可用于描绘弧线和曲线。  
  
 由于 <xref:System.Windows.Media.Geometry> 是一种 <xref:System.Windows.Freezable> 类型，因此 <xref:System.Windows.Media.Geometry> 对象提供几个特殊功能：可声明为[资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)、可在多个对象之间共享、可设为只读以提高性能、可进行克隆以及可设为线程安全对象。  有关 <xref:System.Windows.Freezable> 对象提供的不同功能的更多信息，请参见 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
<a name="wcpsdk_graphics_geometry_geometryandshapes"></a>   
## 几何图形与形状  
 <xref:System.Windows.Media.Geometry> 和 <xref:System.Windows.Shapes.Shape> 类的相似之处在于它们均描绘二维形状（例如，比较 <xref:System.Windows.Media.EllipseGeometry> 和 <xref:System.Windows.Shapes.Ellipse>），但它们之间存在一些重要的区别。  
  
 其一，<xref:System.Windows.Media.Geometry> 类继承自 <xref:System.Windows.Freezable> 类，而 <xref:System.Windows.Shapes.Shape> 类则继承自 <xref:System.Windows.FrameworkElement>。  因为 <xref:System.Windows.Shapes.Shape> 对象是元素，所以它们可以进行自我呈现并参与布局系统，而 <xref:System.Windows.Media.Geometry> 对象则不能。  
  
 尽管 <xref:System.Windows.Shapes.Shape> 对象比 <xref:System.Windows.Media.Geometry> 对象更易于使用，但 <xref:System.Windows.Media.Geometry> 对象更通用。  尽管 <xref:System.Windows.Shapes.Shape> 对象用于呈现二维图形，但 <xref:System.Windows.Media.Geometry> 对象可用于为二维图形定义几何区域、定义剪辑区域或者定义命中测试区域等等。  
  
### Path 形状  
 一个 <xref:System.Windows.Shapes.Shape>，即 <xref:System.Windows.Shapes.Path> 类实际使用 <xref:System.Windows.Media.Geometry> 来描绘它的内容。  通过使用 <xref:System.Windows.Media.Geometry> 设置 <xref:System.Windows.Shapes.Path> 的 <xref:System.Windows.Shapes.Path.Data%2A> 属性以及设置它的 <xref:System.Windows.Shapes.Shape.Fill%2A> 和 <xref:System.Windows.Shapes.Shape.Stroke%2A> 属性，可以呈现 <xref:System.Windows.Media.Geometry>。  
  
<a name="commonproperties"></a>   
## 采用 Geometry 的常见属性  
 前面几部分提到 Geometry 对象可以与其他对象一起使用以实现多种用途，例如，绘制形状、进行动画处理以及剪辑。  下表列出了几个类，这几个类都具有采用 <xref:System.Windows.Media.Geometry> 对象的属性。  
  
|类型|属性|  
|--------|--------|  
|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.PathGeometry%2A>|  
|<xref:System.Windows.Media.DrawingGroup>|<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>|  
|<xref:System.Windows.Media.GeometryDrawing>|<xref:System.Windows.Media.GeometryDrawing.Geometry%2A>|  
|<xref:System.Windows.Shapes.Path>|<xref:System.Windows.Shapes.Path.Data%2A>|  
|<xref:System.Windows.UIElement>|<xref:System.Windows.UIElement.Clip%2A>|  
  
<a name="wcpsdk_graphics_geometry_geometrytypes"></a>   
## 简单的几何图形类型  
 所有几何图形的基类都是抽象类 <xref:System.Windows.Media.Geometry>。  派生自 <xref:System.Windows.Media.Geometry> 类的类大致可以分为三个类别：简单的几何图形、路径几何图形以及复合几何图形。  
  
 简单的几何图形类包括 <xref:System.Windows.Media.LineGeometry>、<xref:System.Windows.Media.RectangleGeometry> 和 <xref:System.Windows.Media.EllipseGeometry>，用于创建基本的几何形状，如直线、矩形和圆。  
  
-   <xref:System.Windows.Media.LineGeometry> 通过指定直线的起点和终点来定义。  
  
-   <xref:System.Windows.Media.RectangleGeometry> 使用 <xref:System.Windows.Rect> 结构来定义，该结构指定它的相对位置以及它的高度和宽度。  您可以通过设置 <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> 和 <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> 属性来创建圆角矩形。  
  
-   <xref:System.Windows.Media.EllipseGeometry> 通过中心点、x 半径和 y 半径来定义。  下面的示例演示如何创建简单的几何图形来进行呈现和剪辑。  
  
 可以使用 <xref:System.Windows.Media.PathGeometry> 或者通过将 Geometry 对象组合在一起来创建这些形状以及更复杂的形状，但是这些类提供了一种生成这些基本的几何形状的更简单方式。  
  
 下面的示例演示如何创建并呈现 <xref:System.Windows.Media.LineGeometry>。  前面已提到，<xref:System.Windows.Media.Geometry> 对象无法进行自我绘制，因此本示例使用 <xref:System.Windows.Shapes.Path> 形状来呈现直线。  因为直线没有面积，设置 <xref:System.Windows.Shapes.Path> 的 <xref:System.Windows.Shapes.Shape.Fill%2A> 属性没有任何效果；因此仅指定 <xref:System.Windows.Shapes.Shape.Stroke%2A> 和 <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> 属性。  下面的插图显示此示例的输出。  
  
 ![一个 LineGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-line.png "graphicsmm\_line")  
从 \(10,20\) 绘制到 \(100,130\) 的 LineGeometry  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMLineGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmlinegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmlinegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmlinegeometryexample)]  
  
 下一个示例演示如何创建并呈现 <xref:System.Windows.Media.EllipseGeometry>。  该示例将 <xref:System.Windows.Media.EllipseGeometry> 的 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 设置为点 `50,50`，将 x 半径和 y 半径均设置为 `50`，这将创建一个直径为 100 的圆。  通过为 Path 元素的 Fill 属性赋予一个值（在本例中为 <xref:System.Windows.Media.Brushes.Gold%2A>）来绘制椭圆的内部。  下面的插图显示此示例的输出。  
  
 ![一个 EllipseGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-ellipse.png "graphicsmm\_ellipse")  
绘制在 \(50,50\) 处的 EllipseGeometry  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMEllipseGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmellipsegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMEllipseGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmellipsegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMEllipseGeometryExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmellipsegeometryexample)]  
  
 下面的示例演示如何创建和呈现 <xref:System.Windows.Media.RectangleGeometry>。  矩形的位置和尺寸由 <xref:System.Windows.Rect> 结构定义。  位置是 `50,50`，高度和宽度均为 `25`，这将创建一个正方形。  下面的插图显示此示例的输出。  
  
 ![一个 RectangleGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rectangle.png "graphicsmm\_rectangle")  
绘制在 50,50 处的 RectangleGeometry  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMRectangleGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmrectanglegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmrectanglegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmrectanglegeometryexample)]  
  
 下面的示例演示如何将 <xref:System.Windows.Media.EllipseGeometry> 用作图像的剪辑区域。  用 <xref:System.Windows.FrameworkElement.Width%2A> 200 和 <xref:System.Windows.FrameworkElement.Height%2A> 150 定义了一个 <xref:System.Windows.Controls.Image> 对象。  一个 <xref:System.Windows.Media.EllipseGeometry.RadiusX%2A> 值为 100、<xref:System.Windows.Media.EllipseGeometry.RadiusY%2A> 值为 75、<xref:System.Windows.Media.EllipseGeometry.Center%2A> 值为 100,75 的 <xref:System.Windows.Media.EllipseGeometry> 设置为图像的 <xref:System.Windows.UIElement.Clip%2A> 属性。  图像中只有位于椭圆区域内部的部分才会显示。  下面的插图显示此示例的输出。  
  
 ![具有剪辑和没有剪辑的图像](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-clipexample.png "graphicsmm\_clipexample")  
用于剪辑 Image 控件的 EllipseGeometry  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMImageClipGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmimageclipgeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMImageClipGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmimageclipgeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMImageClipGeometryExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmimageclipgeometryexample)]  
  
<a name="wcpsdk_graphics_geometry_pathgeometry"></a>   
## PathGeometry  
 <xref:System.Windows.Media.PathGeometry> 类及其轻型等效项 <xref:System.Windows.Media.StreamGeometry> 类提供了描绘由弧线、曲线和直线组成的多个复杂图形的方法。  
  
 <xref:System.Windows.Media.PathGeometry> 的核心是 <xref:System.Windows.Media.PathFigure> 对象的集合；这些对象之所以这样命名是因为每个图形都描绘 <xref:System.Windows.Media.PathGeometry> 中的一个离散形状。  每个 <xref:System.Windows.Media.PathFigure> 自身又由一个或多个 <xref:System.Windows.Media.PathSegment> 对象组成，每个这样的对象均描绘图形的一条线段。  
  
 线段有多种类型。  
  
|线段类型|说明|示例|  
|----------|--------|--------|  
|<xref:System.Windows.Media.ArcSegment>|在两个点之间创建一条椭圆弧线。|[创建椭圆弧](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-an-elliptical-arc.md).|  
|<xref:System.Windows.Media.BezierSegment>|在两个点之间创建一条三次方贝塞尔曲线。|[创建三次方贝塞尔曲线](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-cubic-bezier-curve.md).|  
|<xref:System.Windows.Media.LineSegment>|在两个点之间创建一条直线。|[在 PathGeometry 中创建 LineSegment](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-linesegment-in-a-pathgeometry.md)|  
|<xref:System.Windows.Media.PolyBezierSegment>|创建一系列三次方贝塞尔曲线。|请参见 <xref:System.Windows.Media.PolyBezierSegment> 类型页。|  
|<xref:System.Windows.Media.PolyLineSegment>|创建一系列直线。|请参见 <xref:System.Windows.Media.PolyLineSegment> 类型页。|  
|<xref:System.Windows.Media.PolyQuadraticBezierSegment>|创建一系列二次贝塞尔曲线。|请参见 <xref:System.Windows.Media.PolyQuadraticBezierSegment> 页。|  
|<xref:System.Windows.Media.QuadraticBezierSegment>|创建一条二次贝塞尔曲线。|[创建二次贝塞尔曲线](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-quadratic-bezier-curve.md).|  
  
 <xref:System.Windows.Media.PathFigure> 中的线段将合并为一个几何形状，该形状将每一条线段的终点作为下一条线段的起点。  <xref:System.Windows.Media.PathFigure> 的 <xref:System.Windows.Media.PathFigure.StartPoint%2A> 属性指定绘制第一条线段的起始点。  后面的每条线段都以上一条线段的终点作为起点。  例如，通过将 <xref:System.Windows.Media.PathFigure.StartPoint%2A> 属性设置为 `10,50` 并创建 <xref:System.Windows.Media.LineSegment.Point%2A> 属性设置为 `10,150` 的 <xref:System.Windows.Media.LineSegment>，可定义一条从 `10,50` 到 `10,150` 的竖线。  
  
 下面的示例创建由一个 <xref:System.Windows.Media.PathFigure>（具有一个 <xref:System.Windows.Media.LineSegment>）组成的简单 <xref:System.Windows.Media.PathGeometry>，并使用 <xref:System.Windows.Shapes.Path> 元素来显示它。  <xref:System.Windows.Media.PathFigure> 对象的 <xref:System.Windows.Media.PathFigure.StartPoint%2A> 设置为 `10,20`，并用终点 `100,130` 定义一个 <xref:System.Windows.Media.LineSegment>。  下面的插图显示了此示例创建的 <xref:System.Windows.Media.PathGeometry>。  
  
 ![一个 LineGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-line.png "graphicsmm\_line")  
包含一个 LineSegment 的 PathGeometry  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMPathGeometryLineExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmpathgeometrylineexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryLineExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmpathgeometrylineexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryLineExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmpathgeometrylineexample)]  
  
 有必要将此示例与前面的 <xref:System.Windows.Media.LineGeometry> 示例进行比较。  <xref:System.Windows.Media.PathGeometry> 使用的语法比简单的 <xref:System.Windows.Media.LineGeometry> 使用的语法要详细得多，在本例中使用 <xref:System.Windows.Media.LineGeometry> 类可能更有效，但是使用 <xref:System.Windows.Media.PathGeometry> 的详细语法可以创建极其复杂的几何区域。  
  
 使用 <xref:System.Windows.Media.PathSegment> 对象的组合可以创建更复杂的几何图形。  
  
 下一个示例使用一个 <xref:System.Windows.Media.BezierSegment>、一个 <xref:System.Windows.Media.LineSegment> 以及一个 <xref:System.Windows.Media.ArcSegment> 来创建形状。  该示例首先通过定义四个点来创建一个三次方贝塞尔曲线：起点（前一条线段的终点）、终点 \(<xref:System.Windows.Media.BezierSegment.Point3%2A>\) 以及两个控制点（<xref:System.Windows.Media.BezierSegment.Point1%2A> 和 <xref:System.Windows.Media.BezierSegment.Point2%2A>）。  三次方贝塞尔曲线的两个控制点的作用像磁铁一样，朝着自身的方向吸引本应为直线的部分，从而形成一条曲线。  第一个控制点 <xref:System.Windows.Media.BezierSegment.Point1%2A> 影响曲线的开始部分；第二个控制点 <xref:System.Windows.Media.BezierSegment.Point2%2A> 影响曲线的结束部分。  
  
 然后该示例添加一个 <xref:System.Windows.Media.LineSegment>，该线段从前面的 <xref:System.Windows.Media.BezierSegment> 的终点绘制到它的 <xref:System.Windows.Media.LineSegment> 属性所指定的点。  
  
 然后该示例添加一个 <xref:System.Windows.Media.ArcSegment>，该线段从前面的 <xref:System.Windows.Media.LineSegment> 的终点绘制到它的 <xref:System.Windows.Media.ArcSegment.Point%2A> 属性所指定的点。  该示例还指定弧线的 x 半径和 y 半径 \(<xref:System.Windows.Media.ArcSegment.Size%2A>\)、旋转角度 \(<xref:System.Windows.Media.ArcSegment.RotationAngle%2A>\)、指示最终弧线的角度应为多大的标志 \(<xref:System.Windows.Media.ArcSegment.IsLargeArc%2A>\) 以及指示弧线绘制方向的值 \(<xref:System.Windows.Media.ArcSegment.SweepDirection%2A>\)。  下面的插图显示了此示例创建的形状。  
  
 ![一个 PathGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-path2.png "graphicsmm\_path2")  
PathGeometry  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMPathGeometryComplexExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmpathgeometrycomplexexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmpathgeometrycomplexexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmpathgeometrycomplexexample)]  
  
 通过在一个 <xref:System.Windows.Media.PathGeometry> 内使用多个 <xref:System.Windows.Media.PathFigure> 对象，可以创建更复杂的几何图形。  
  
 下面的示例创建一个具有两个 <xref:System.Windows.Media.PathFigure> 对象的 <xref:System.Windows.Media.PathGeometry>，其中每个对象均包含多个 <xref:System.Windows.Media.PathSegment> 对象。  使用了上面的示例中的 <xref:System.Windows.Media.PathFigure> 以及具有一个 <xref:System.Windows.Media.PolyLineSegment> 和一个 <xref:System.Windows.Media.QuadraticBezierSegment> 的 <xref:System.Windows.Media.PathFigure>。  <xref:System.Windows.Media.PolyLineSegment> 是用一个点数组定义的，<xref:System.Windows.Media.QuadraticBezierSegment> 是用一个控制点和一个终点定义的。  下面的插图显示了此示例创建的形状。  
  
 ![一个 PathGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-path.png "graphicsmm\_path")  
具有多个图形的 PathGeometry  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMPathGeometryComplexMultiExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmpathgeometrycomplexmultiexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexMultiExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmpathgeometrycomplexmultiexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexMultiExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmpathgeometrycomplexmultiexample)]  
  
### StreamGeometry  
 与 <xref:System.Windows.Media.PathGeometry> 类类似，<xref:System.Windows.Media.StreamGeometry> 定义一个可以包含曲线、弧线和直线的复杂几何形状。  与 <xref:System.Windows.Media.PathGeometry> 不同，<xref:System.Windows.Media.StreamGeometry> 的内容不支持数据绑定、动画或修改。  当您需要描绘复杂的几何图形，但不希望因为支持数据绑定、动画或修改而引入系统开销时，可使用 <xref:System.Windows.Media.StreamGeometry>。  由于它的高效，<xref:System.Windows.Media.StreamGeometry> 类是描绘装饰物的理想选择。  
  
 有关示例，请参见[使用 StreamGeometry 创建形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-using-a-streamgeometry.md)。  
  
### 路径标记语法  
 <xref:System.Windows.Media.PathGeometry> 和 <xref:System.Windows.Media.StreamGeometry> 类型使用一系列特殊的移动和绘制命令来支持[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 特性语法。  有关更多信息，请参见[路径标记语法](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)。  
  
<a name="wcpsdk_graphics_geometry_introduction2"></a>   
## 复合几何图形  
 使用 <xref:System.Windows.Media.GeometryGroup>、<xref:System.Windows.Media.CombinedGeometry> 或者通过调用静态的 <xref:System.Windows.Media.Geometry> 方法 <xref:System.Windows.Media.Geometry.Combine%2A>，可以创建复合几何图形对象。  
  
-   <xref:System.Windows.Media.CombinedGeometry> 对象和 <xref:System.Windows.Media.Geometry.Combine%2A> 方法执行布尔操作，以组合两个几何图形所定义的面积。  没有面积的<xref:System.Windows.Media.Geometry> 对象将被丢弃。  只能组合两个 <xref:System.Windows.Media.Geometry> 对象（但是这两个几何图形也可以是复合几何图形）。  
  
-   <xref:System.Windows.Media.GeometryGroup> 类创建它所包含的 <xref:System.Windows.Media.Geometry> 对象的组合体，但不合并其面积。  可以向 <xref:System.Windows.Media.GeometryGroup> 中添加任意数量的 <xref:System.Windows.Media.Geometry> 对象。  有关示例，请参见[创建复合形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-composite-shape.md)。  
  
 因为它们不执行合并操作，所以使用 <xref:System.Windows.Media.GeometryGroup> 对象的性能比使用 <xref:System.Windows.Media.CombinedGeometry> 对象或 <xref:System.Windows.Media.Geometry.Combine%2A> 方法的性能高。  
  
<a name="combindgeometriessection"></a>   
## 组合的几何图形  
 前面一节提到，<xref:System.Windows.Media.CombinedGeometry> 对象和 <xref:System.Windows.Media.Geometry.Combine%2A> 方法合并它们包含的几何图形所定义的面积。  <xref:System.Windows.Media.GeometryCombineMode> 枚举指定如何组合几何图形。  <xref:System.Windows.Media.CombinedGeometry.GeometryCombineMode%2A> 属性的可能值有：<xref:System.Windows.Media.GeometryCombineMode>、<xref:System.Windows.Media.GeometryCombineMode>、<xref:System.Windows.Media.GeometryCombineMode> 和 <xref:System.Windows.Media.GeometryCombineMode>。  
  
 在下面的示例中，用 Union 组合模式定义了一个 <xref:System.Windows.Media.CombinedGeometry>。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 和 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 定义为相同半径的圆，但是中心偏离 50。  
  
 [!code-xml[GeometrySample#23](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#23)]  
  
 ![“联合”组合模式的结果](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-union.png "mil\_task\_combined\_geometry\_union")  
  
 在下面的示例中，用 <xref:System.Windows.Media.GeometryCombineMode> 组合模式定义了一个 <xref:System.Windows.Media.CombinedGeometry>。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 和 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 定义为相同半径的圆，但是中心偏离 50。  
  
 [!code-xml[GeometrySample#24](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#24)]  
  
 ![Xor 组合模式的结果](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-xor.png "mil\_task\_combined\_geometry\_xor")  
  
 有关其他示例，请参见 [创建复合形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-composite-shape.md) 和 [创建组合的几何图形](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-combined-geometry.md)。  
  
<a name="freezable_features"></a>   
## Freezable 功能  
 由于 <xref:System.Windows.Media.Geometry> 类继承自 <xref:System.Windows.Freezable> 类，因此它提供了几个特殊功能：<xref:System.Windows.Media.Geometry> 对象可按[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)中的方式进行声明、在多个对象之间共享、设为只读以提高性能、进行克隆以及设为线程安全。  有关 <xref:System.Windows.Freezable> 对象提供的不同功能的更多信息，请参见 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
<a name="othergeometryfeatures"></a>   
## 其他 Geometry 功能  
 <xref:System.Windows.Media.Geometry> 类还提供有用的实用程序方法，例如：  
  
-   <xref:System.Windows.Media.Geometry.GetArea%2A> \- 获取 <xref:System.Windows.Media.Geometry> 的面积。  
  
-   <xref:System.Windows.Media.Geometry.FillContains%2A> \- 确定该 Geometry 是否包含其他 <xref:System.Windows.Media.Geometry>。  
  
-   <xref:System.Windows.Media.Geometry.StrokeContains%2A> \- 确定 <xref:System.Windows.Media.Geometry> 的笔画是否包含指定的点。  
  
 有关其方法的完整列表，请参见 <xref:System.Windows.Media.Geometry> 类。  
  
## 请参阅  
 <xref:System.Windows.Media.Geometry>   
 <xref:System.Windows.Media.PathGeometry>   
 <xref:System.Windows.Shapes.Path>   
 <xref:System.Windows.Media.GeometryDrawing>   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [路径标记语法](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/geometries-how-to-topics.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [WPF 中的形状和基本绘图概述](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)