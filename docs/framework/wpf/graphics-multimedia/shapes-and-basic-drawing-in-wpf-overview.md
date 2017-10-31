---
title: "WPF 中的形状和基本绘图概述 | Microsoft Docs"
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
  - "基本绘制"
  - "Shape 对象"
  - "形状, 关于形状"
  - "向量绘制, 概述"
  - "向量, 绘图"
ms.assetid: 66d7a6d6-e3b6-47bc-8dfe-8a1b26f7d901
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# WPF 中的形状和基本绘图概述
本主题概述如何使用 <xref:System.Windows.Shapes.Shape> 对象绘图。  <xref:System.Windows.Shapes.Shape> 是一种允许您在屏幕中绘制形状的 <xref:System.Windows.UIElement> 类型。  由于它们是 UI 元素，因此 <xref:System.Windows.Shapes.Shape> 对象可以在 <xref:System.Windows.Controls.Panel> 元素和大多数控件中使用。  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供了对图形和呈现服务的若干层访问。  在顶层，<xref:System.Windows.Shapes.Shape> 对象很容易使用，并且提供了许多有用功能，例如布局和参与 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 事件系统。  
  
   
  
<a name="shapes"></a>   
## 形状对象  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了许多易于使用的 <xref:System.Windows.Shapes.Shape> 对象。  所有形状对象都是从 <xref:System.Windows.Shapes.Shape> 类继承的。  可用的 Shape 对象包括 <xref:System.Windows.Shapes.Ellipse>、<xref:System.Windows.Shapes.Line>、<xref:System.Windows.Shapes.Path>、<xref:System.Windows.Shapes.Polygon>、<xref:System.Windows.Shapes.Polyline> 和 <xref:System.Windows.Shapes.Rectangle>。<xref:System.Windows.Shapes.Shape> 对象共享以下通用属性。  
  
-   <xref:System.Windows.Shapes.Shape.Stroke%2A>：说明如何绘制形状的轮廓。  
  
-   <xref:System.Windows.Shapes.Shape.StrokeThickness%2A>：说明形状轮廓的粗细。  
  
-   <xref:System.Windows.Shapes.Shape.Fill%2A>：说明如何绘制形状的内部。  
  
-   用于指定坐标和顶点的数据属性，以[与设备无关的像素](GTMT)来度量。  
  
 由于形状对象派生于 <xref:System.Windows.UIElement>，因此可以在面板和大多数控件中使用。  <xref:System.Windows.Controls.Canvas> 面板是用于创建复杂绘图的特别理想的选择，因为它支持对其子对象的绝对定位。  
  
 使用 <xref:System.Windows.Shapes.Line> 类可以在两个点之间绘制一条直线。  下面的示例演示了几种指定线条坐标和描边属性的方法。  
  
 [!code-xml[drawingwithshapeelements#LineExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/lineexample.xaml#lineexample1)]  
  
 [!code-cpp[shapesprocedural#ShapesProceduralLine](../../../../samples/snippets/cpp/VS_Snippets_Wpf/ShapesProcedural/CPP/ShapesProcedural.cpp#shapesproceduralline)]
 [!code-csharp[shapesprocedural#ShapesProceduralLine](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ShapesProcedural/Csharp/ShapesProcedural.cs#shapesproceduralline)]
 [!code-vb[shapesprocedural#ShapesProceduralLine](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ShapesProcedural/VisualBasic/ShapesProceduralVB.vb#shapesproceduralline)]  
  
 下图显示了所呈现的 <xref:System.Windows.Shapes.Line>。  
  
 ![直线图示](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-line2.png "shape\_ovw\_line2")  
  
 虽然 <xref:System.Windows.Shapes.Line> 类提供了 <xref:System.Windows.Shapes.Shape.Fill%2A> 属性，但设置该属性无效，因为 <xref:System.Windows.Shapes.Line> 没有区域。  
  
 另一个常用形状是 <xref:System.Windows.Shapes.Ellipse>。  通过定义形状的 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性来创建 <xref:System.Windows.Shapes.Ellipse>。  若要绘制一个圆，请指定一个其 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 值相等的 <xref:System.Windows.Shapes.Ellipse>。  
  
 [!code-xml[ShapeOverviews#ShapesOVW1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ShapeOverviews/CS/Window1.xaml#shapesovw1)]  
  
 [!code-csharp[brushesmiscsnippets_procedural_snip#SetBackgroundColorOfShapeCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesMiscSnippets_procedural_snip/CSharp/SetBackgroundColorOfShapeExample.cs#setbackgroundcolorofshapecodeexamplewholepage)]
 [!code-vb[brushesmiscsnippets_procedural_snip#SetBackgroundColorOfShapeCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesMiscSnippets_procedural_snip/visualbasic/setbackgroundcolorofshapeexample.vb#setbackgroundcolorofshapecodeexamplewholepage)]  
  
 下图显示了一个已呈现 <xref:System.Windows.Shapes.Ellipse> 的示例。  
  
 ![椭圆图示](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-ellipse2.png "shape\_ovw\_ellipse2")  
  
<a name="paths"></a>   
## 使用 Path 和 Geometry  
 使用 <xref:System.Windows.Shapes.Path> 类可以绘制曲线和复杂形状。  这些曲线和形状使用 <xref:System.Windows.Media.Geometry> 对象来说明  若要使用 <xref:System.Windows.Shapes.Path>，请创建一个 <xref:System.Windows.Media.Geometry> 并使用它来设置 <xref:System.Windows.Shapes.Path> 对象的 <xref:System.Windows.Shapes.Path.Data%2A> 属性。  
  
 可以从各种 <xref:System.Windows.Media.Geometry> 对象中进行选择。  <xref:System.Windows.Media.LineGeometry>、<xref:System.Windows.Media.RectangleGeometry> 和 <xref:System.Windows.Media.EllipseGeometry> 类说明了相对简单的形状。  若要创建更复杂的形状或创建曲线，请使用 <xref:System.Windows.Media.PathGeometry>。  
  
<a name="pathgeometry"></a>   
### PathGeometry 和 PathSegment  
 <xref:System.Windows.Media.PathGeometry> 对象由一个或多个 <xref:System.Windows.Media.PathFigure> 对象组成；每个 <xref:System.Windows.Media.PathFigure> 代表一个不同的“图形”或形状。  每个 <xref:System.Windows.Media.PathFigure> 自身又由一个或多个 <xref:System.Windows.Media.PathSegment> 对象组成，每个对象均代表图形或形状的已连接部分。  Segment 类型包括 <xref:System.Windows.Media.LineSegment>、<xref:System.Windows.Media.BezierSegment> 和 <xref:System.Windows.Media.ArcSegment>。  
  
 在下面的示例中，使用一个 <xref:System.Windows.Shapes.Path> 来绘制二次方贝塞尔曲线。  
  
 [!code-xml[geometrysample#34](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#34)]  
  
 下图显示了所呈现的形状。  
  
 ![路径图示](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-path2.png "shape\_ovw\_path2")  
  
 有关 <xref:System.Windows.Media.PathGeometry> 和其他 <xref:System.Windows.Media.Geometry> 类的更多信息，请参见 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)。  
  
<a name="pathdatastring"></a>   
### XAML 缩写语法  
 在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中，还可以使用一种特殊的缩写语法来说明 <xref:System.Windows.Shapes.Path>。  在下面的示例中，使用缩写语法来绘制一个复杂形状。  
  
```xaml  
<Path Stroke="DarkGoldenRod" StrokeThickness="3"   
Data="M 100,200 C 100,25 400,350 400,175 H 280" />  
```  
  
 下面的图像显示了一个已呈现的 <xref:System.Windows.Shapes.Path>。  
  
 ![路径图示](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-path.png "shape\_ovw\_path")  
  
 <xref:System.Windows.Shapes.Path.Data%2A> 特性字符串以“moveto”命令开头（由 M 指示），它为 <xref:System.Windows.Controls.Canvas> 的坐标系统中的路径建立一个起点。  <xref:System.Windows.Shapes.Path> 数据参数区分大小写。  大写的 M 指示新的当前点的绝对位置。  小写 m 则指示相对坐标。  第一段是一个三次方[贝塞尔曲线](GTMT)，该曲线从 \(100,200\) 开始，在 \(400,175\) 结束，使用 \(100,25\) 和 \(400,350\) 这两个控制点绘制。  此段由 <xref:System.Windows.Shapes.Path.Data%2A> 特性字符串中的 C 命令指示。  同样，大写的 C 指示绝对路径；小写的 c 则指示相对路径。  
  
 第二段以绝对水平“lineto”命令 H 开头，它指定绘制一条从前面的子路径的终结点 \(400,175\) 到新终结点 \(280,175\) 的直线。  由于它是一个水平“lineto”命令，因此指定的值是 *x* 坐标。  
  
 有关完整的路径语法，请参见 <xref:System.Windows.Shapes.Path.Data%2A> 参考内容和[使用 PathGeometry 创建形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md)。  
  
<a name="fillpaint"></a>   
## 绘制形状  
 <xref:System.Windows.Media.Brush> 对象用于绘制形状的 <xref:System.Windows.Shapes.Shape.Stroke%2A> 和 <xref:System.Windows.Shapes.Shape.Fill%2A>。  在下面的示例中，指定了 <xref:System.Windows.Shapes.Ellipse> 的描边和填充。  请注意，画笔属性的有效输入可以是关键字或十六进制颜色值。  有关可用的颜色关键字的更多信息，请参见 <xref:System.Windows.Media> 命名空间中 <xref:System.Windows.Media.Colors> 类的属性。  
  
```  
  
<Canvas Background="LightGray">   
   <Ellipse  
      Canvas.Top="50"  
      Canvas.Left="50"  
      Fill="#FFFFFF00"  
      Height="75"  
      Width="75"  
      StrokeThickness="5"  
      Stroke="#FF0000FF"/>  
</Canvas>  
  
```  
  
 下图显示了所呈现的 <xref:System.Windows.Shapes.Ellipse>。  
  
 ![椭圆](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-ellipsefill.png "shape\_ovw\_ellipsefill")  
  
 您也可以使用属性元素语法显式创建一个 <xref:System.Windows.Media.SolidColorBrush> 对象，以使用纯色绘制形状。  
  
```  
  
<!-- This polygon shape uses pre-defined color values for its Stroke and  
     Fill properties.   
     The SolidColorBrush's Opacity property affects the fill color in   
     this case by making it slightly transparent (opacity of 0.4) so   
     that it blends with any underlying color. -->  
  
<Polygon  
    Points="300,200 400,125 400,275 300,200"  
    Stroke="Purple"   
    StrokeThickness="2">  
    <Polygon.Fill>  
       <SolidColorBrush Color="Blue" Opacity="0.4"/>  
    </Polygon.Fill>  
</Polygon>  
```  
  
 下图显示呈现的形状。  
  
 ![SolidColorBrush 图示](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-solidcolorbrush.png "shape\_ovw\_solidcolorbrush")  
  
 还可以绘制形状的带有渐变、图像、图案等效果的描边或填充。  有关更多信息，请参见 [使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)。  
  
<a name="stretchableshapessection"></a>   
## 可拉伸形状  
 <xref:System.Windows.Shapes.Line>、<xref:System.Windows.Shapes.Path>、<xref:System.Windows.Shapes.Polygon>、<xref:System.Windows.Shapes.Polyline> 和 <xref:System.Windows.Shapes.Rectangle> 类都有一个 <xref:System.Windows.Shapes.Shape.Stretch%2A> 属性。  该属性确定如何拉伸 <xref:System.Windows.Shapes.Shape> 对象的内容（要绘制的形状）以填充 <xref:System.Windows.Shapes.Shape> 对象的布局空间。  <xref:System.Windows.Shapes.Shape> 对象的布局空间是布局系统分配给 <xref:System.Windows.Shapes.Shape>（根据显式的 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 设置，或其 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 和 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 设置）的空间量。  有关 Windows Presentation Foundation 中的布局的更多信息，请参见[布局](../../../../docs/framework/wpf/advanced/layout.md)概述。  
  
 Stretch 属性使用以下值之一：  
  
-   <xref:System.Windows.Media.Stretch>：不拉伸 <xref:System.Windows.Shapes.Shape> 对象的内容。  
  
-   <xref:System.Windows.Media.Stretch>：拉伸 <xref:System.Windows.Shapes.Shape> 对象的内容以填充其布局空间。  不保留长宽比。  
  
-   <xref:System.Windows.Media.Stretch>：尽可能地拉伸 <xref:System.Windows.Shapes.Shape> 对象的内容以填充其布局空间，同时保留其原始长宽比。  
  
-   <xref:System.Windows.Media.Stretch>：完全拉伸 <xref:System.Windows.Shapes.Shape> 对象的内容以填充其布局空间，同时保留其原始长宽比。  
  
 请注意，在拉伸 <xref:System.Windows.Shapes.Shape> 对象的内容时，会在拉伸之后绘制 <xref:System.Windows.Shapes.Shape> 对象的轮廓。  
  
 在下面的示例中，使用一个 <xref:System.Windows.Shapes.Polygon> 从 \(0,0\) 到 \(0,1\)，再到 \(1,1\) 绘制一个非常小的三角形。  <xref:System.Windows.Shapes.Polygon> 对象的 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 设置为 100，其拉伸属性设置为 Fill。  结果是，将拉伸 <xref:System.Windows.Shapes.Polygon> 对象的内容（三角形）以填充更大的空间。  
  
```  
...  
<Polygon  
  Points="0,0 0,1 1,1"  
  Fill="Blue"  
  Width="100"  
  Height="100"  
  Stretch="Fill"  
  Stroke="Black"  
  StrokeThickness="2" />  
...  
```  
  
```  
...  
PointCollection myPointCollection = new PointCollection();  
myPointCollection.Add(new Point(0,0));  
myPointCollection.Add(new Point(0,1));  
myPointCollection.Add(new Point(1,1));  
  
Polygon myPolygon = new Polygon();  
myPolygon.Points = myPointCollection;  
myPolygon.Fill = Brushes.Blue;  
myPolygon.Width = 100;  
myPolygon.Height = 100;  
myPolygon.Stretch = Stretch.Fill;  
myPolygon.Stroke = Brushes.Black;  
myPolygon.StrokeThickness = 2;  
...  
```  
  
<a name="transforms"></a>   
## 变换形状  
 <xref:System.Windows.Media.Transform> 类提供了在二维平面中变换形状的方法。  不同类型的变换包括旋转 \(<xref:System.Windows.Media.RotateTransform>\)、缩放 \(<xref:System.Windows.Media.ScaleTransform>\)、斜切 \(<xref:System.Windows.Media.SkewTransform>\) 和转换 \(<xref:System.Windows.Media.TranslateTransform>\)。  
  
 经常应用于形状的变换操作是旋转。  若要旋转形状，请创建一个 <xref:System.Windows.Media.RotateTransform> 并指定其 <xref:System.Windows.Media.RotateTransform.Angle%2A>。  45 度的 <xref:System.Windows.Media.RotateTransform.Angle%2A> 将元素沿顺时针方向旋转 45 度；90 度将元素沿顺时针方向旋转 90 度；依此类推。  如果您要控制元素的旋转点，请设置 <xref:System.Windows.Media.RotateTransform.CenterX%2A> 和 <xref:System.Windows.Media.RotateTransform.CenterY%2A> 属性。  这些属性值以要变换元素的坐标空间表示。  <xref:System.Windows.Media.RotateTransform.CenterX%2A> 和 <xref:System.Windows.Media.RotateTransform.CenterY%2A> 具有默认值零。  最后，将 <xref:System.Windows.Media.RotateTransform> 应用于该元素。  如果您不希望变形影响到布局，请设置形状的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性。  
  
 在下面的示例中，使用 <xref:System.Windows.Media.RotateTransform> 将形状围绕其左上角 \(0,0\) 旋转 45 度。  
  
 [!code-xml[transformssample#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/RotateTransformExample.xaml#14)]  
  
 在下一个示例中，另一个形状将旋转 45 度，但这一次围绕点 \(25,50\) 进行旋转。  
  
 [!code-xml[transformssample#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/RotateTransformExample.xaml#15)]  
  
 下图显示了应用这两种变形的结果。  
  
 ![以不同中心点进行的 45 度旋转](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-rotatetransform45degrees.png "wcpsdk\_graphicsmm\_rotatetransform45degrees")  
  
 在上一个示例中，向每个形状对象应用了一次变形。  若要向一个形状（或任何其他 UI 元素）应用多次变形，请使用 <xref:System.Windows.Media.TransformGroup>。  
  
## 请参阅  
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [演练：开始使用 WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)