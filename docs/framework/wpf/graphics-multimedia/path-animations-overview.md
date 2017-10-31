---
title: "路径动画概述 | Microsoft Docs"
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
  - "路径动画"
  - "路径动画"
ms.assetid: 979c732c-df74-47a6-be96-8e07b3707d53
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 路径动画概述
<a name="introduction"></a>本主题介绍路径动画，使您能够使用几何路径来生成输出值。 路径动画可用于移动和旋转对象沿复杂的路径。  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>先决条件  
 若要了解本主题，您应熟悉[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]动画功能。 动画功能的简介，请参阅[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
 因为您使用<xref:System.Windows.Media.PathGeometry>对象来定义一个路径的动画，您还应熟悉<xref:System.Windows.Media.PathGeometry>和不同类型的<xref:System.Windows.Media.PathSegment>对象。 有关详细信息，请参阅[Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)。  
  
<a name="what_is_a_path_animation"></a>   
## <a name="what-is-a-path-animation"></a>路径动画是什么？  
 路径动画是一种<xref:System.Windows.Media.Animation.AnimationTimeline> ，它使用<xref:System.Windows.Media.PathGeometry>作为其输入。 而不是设置 From、 To 或 By 属性 (如替 From/To/By 动画) 或使用关键帧 （与您用于关键帧动画），您定义的几何路径并使用它来设置`PathGeometry`路径动画的属性。 在路径动画运行时，它从路径中读取 x、 y 和角度信息并使用该信息来生成其输出。  
  
 路径动画是对于沿着复杂路径对对象进行动画处理非常有用。 移动路径上的位置的对象是要使用的一种方法<xref:System.Windows.Media.MatrixTransform>和<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>转换沿复杂路径对象。 下面的示例演示这种技术，通过使用<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>对象进行动画处理<xref:System.Windows.Media.MatrixTransform.Matrix%2A>属性<xref:System.Windows.Media.MatrixTransform>。 <xref:System.Windows.Media.MatrixTransform>应用于一个按钮，并且会导致它沿曲线路径移动。 因为<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A>属性设置为`true`，矩形就会旋转沿该路径的正切值。  
  
 [!code-xml[PathAnimationGallery_snippet#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathdoesrotatewithtangentexample.xaml#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathDoesRotateWithTangentExample.cs#matrixanimationusingpathdoesrotatewithtangentwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathDoesRotateWithTangentExample.vb#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 有关详细信息中使用的路径语法[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]示例中，请参阅[路径标记语法](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)概述。 有关完整的示例，请参阅[路径动画示例](http://go.microsoft.com/fwlink/?LinkID=160028)。  
  
 通过使用应用于属性路径动画<xref:System.Windows.Media.Animation.Storyboard>中[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]和代码，或通过使用<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>代码中的方法。 路径动画还可用来创建<xref:System.Windows.Media.Animation.AnimationClock>并将其应用到一个或多个属性。 有关应用动画的不同方法的详细信息，请参阅[属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)。  
  
<a name="animation_types"></a>   
## <a name="path-animation-types"></a>路径动画类型  
 由于动画生成属性值，有不同的属性类型的不同的动画类型。 采用属性进行动画处理<xref:System.Double> (如<xref:System.Windows.Media.TranslateTransform.X%2A>属性<xref:System.Windows.Media.TranslateTransform>)，使用生成的动画<xref:System.Double>值。 采用属性进行动画处理<xref:System.Windows.Point>，使用生成的动画<xref:System.Windows.Point>值，等等。  
  
 路径动画类属于<xref:System.Windows.Media.Animation>命名空间并使用以下命名约定︰  
  
 *<>\>*`AnimationUsingPath`  
  
 其中* <> \> *是该类进行动画处理的值的类型。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]提供以下路径动画类。  
  
|属性类型|相应的路径动画类|示例|  
|-------------------|----------------------------------------|-------------|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|[沿着路径 （双重动画） 对象进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-an-object-along-a-path-double-animation.md)|  
|<xref:System.Windows.Media.Matrix>|<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>|[沿着路径 （矩阵动画） 对象进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-an-object-along-a-path-matrix-animation.md)|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimationUsingPath>|[沿着路径 （点动画） 对象进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-an-object-along-a-path-point-animation.md)|  
  
 一个<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>生成<xref:System.Windows.Media.Matrix>值从其<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.PathGeometry%2A>。 如果用于<xref:System.Windows.Media.MatrixTransform>、 <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>可以移动沿着路径对象。 如果您设置<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A>属性<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>到`true`，它还会沿着路径的曲线的对象。  
  
 一个<xref:System.Windows.Media.Animation.PointAnimationUsingPath>生成<xref:System.Windows.Point>值从 x 坐标和 y 坐标的其<xref:System.Windows.Media.Animation.PointAnimationUsingPath.PathGeometry%2A>。 通过使用<xref:System.Windows.Media.Animation.PointAnimationUsingPath>采用属性进行动画处理<xref:System.Windows.Point>值，可以移动沿着路径对象。 一个<xref:System.Windows.Media.Animation.PointAnimationUsingPath>无法旋转对象。  
  
 一个<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>生成<xref:System.Double>值从其<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.PathGeometry%2A>。 通过设置<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.Source%2A>属性，可以指定是否<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>作为其输出中使用的 x 坐标，y 坐标或路径的角度。 您可以使用<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>来旋转对象或将其移动沿 x 轴或 y 轴。  
  
<a name="pathanimationinput"></a>   
## <a name="path-animation-input"></a>路径动画输入  
 每个路径动画类提供了<xref:System.Windows.Media.PathGeometry>用于指定其输入的属性。 路径动画使用<xref:System.Windows.Media.PathGeometry>来生成其输出值。 <xref:System.Windows.Media.PathGeometry>类允许您描述组成弧线、 曲线和行的多个复杂图形。  
  
 核心<xref:System.Windows.Media.PathGeometry>是一套<xref:System.Windows.Media.PathFigure>对象; 这些对象这样命名是因为每个图描述了中的离散形状<xref:System.Windows.Media.PathGeometry>。 每个<xref:System.Windows.Media.PathFigure>组成一个或多个<xref:System.Windows.Media.PathSegment>对象，其中每个描述该图中的段。  
  
 有许多类型的段。  
  
|段类型|描述|  
|------------------|-----------------|  
|<xref:System.Windows.Media.ArcSegment>|创建两个点之间的椭圆弧。|  
|<xref:System.Windows.Media.BezierSegment>|创建两个点之间的三次方贝塞尔曲线。|  
|<xref:System.Windows.Media.LineSegment>|创建两个点之间的线条。|  
|<xref:System.Windows.Media.PolyBezierSegment>|创建一系列三次方贝塞尔曲线。|  
|<xref:System.Windows.Media.PolyLineSegment>|创建一系列的行。|  
|<xref:System.Windows.Media.PolyQuadraticBezierSegment>|创建一系列的二次贝塞尔曲线。|  
|<xref:System.Windows.Media.QuadraticBezierSegment>|创建二次贝塞尔曲线。|  
  
 中的各段<xref:System.Windows.Media.PathFigure>合并成单一几何形状，它使用段的结束点作为下一段的起始点。 <xref:System.Windows.Media.PathFigure.StartPoint%2A>属性<xref:System.Windows.Media.PathFigure>指定从中提取第一条线段的点。 每个后续段从上一段的结束点开始。 例如，一条竖线从`10,50`到`10,150`可通过设置定义<xref:System.Windows.Media.PathFigure.StartPoint%2A>属性设置为`10,50`和创建<xref:System.Windows.Media.LineSegment>与<xref:System.Windows.Media.LineSegment.Point%2A>的属性的设置`10,150`。  
  
 有关详细信息<xref:System.Windows.Media.PathGeometry>对象，请参阅[Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)。  
  
 在[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，还可以使用特殊的缩写的语法来设置<xref:System.Windows.Media.PathGeometry.Figures%2A>属性<xref:System.Windows.Media.PathGeometry>。 有关详细信息，请参阅[路径标记语法](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)概述。  
  
 有关详细信息中使用的路径语法[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]示例中，请参阅[路径标记语法](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)概述。  
  
## <a name="see-also"></a>另请参阅  
 [路径动画示例](http://go.microsoft.com/fwlink/?LinkID=160028)   
 [路径标记语法](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)   
 [路径动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)