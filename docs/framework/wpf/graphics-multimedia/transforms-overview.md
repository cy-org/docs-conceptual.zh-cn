---
title: "变换概述 | Microsoft Docs"
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
  - "二维转换类"
  - "类, 二维转换"
  - "FrameworkElement 对象, 旋转"
  - "FrameworkElement 对象, 缩放"
  - "FrameworkElement 对象, 扭曲"
  - "FrameworkElement 对象, 转换"
  - "转换类, 二维"
  - "转换, 关于转换"
  - "转换, 关于转换"
ms.assetid: 8f153d5e-ed61-4aa5-a7cd-286f0c427a13
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 变换概述
本主题描述如何使用 [!INCLUDE[TLA#tla_2d](../../../../includes/tlasharptla-2d-md.md)] <xref:System.Windows.Media.Transform> 类来旋转、按比例缩放、移动（平移）和扭曲 <xref:System.Windows.FrameworkElement> 对象。  
  
   
  
<a name="whatIsATransformSection"></a>   
## 什么是变换？  
 <xref:System.Windows.Media.Transform> 定义如何将一个坐标空间中的点映射或变换到另一个坐标空间。  此映射由变换 <xref:System.Windows.Media.Matrix>（一个三行三列的 <xref:System.Double> 值集合）来描述。  
  
> [!NOTE]
>  [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 使用行优先矩阵。  矢量用行矢量（而不是列矢量）表示。  
  
 下表显示了 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 矩阵的结构。  
  
### 二维变换矩阵  
  
||||  
|-|-|-|  
|<xref:System.Windows.Media.Matrix.M11%2A><br /><br /> 默认值：1.0|<xref:System.Windows.Media.Matrix.M12%2A><br /><br /> 默认值：0.0|0.0|  
|<xref:System.Windows.Media.Matrix.M21%2A><br /><br /> 默认值：0.0|<xref:System.Windows.Media.Matrix.M22%2A><br /><br /> 默认值：1.0|0.0|  
|<xref:System.Windows.Media.Matrix.OffsetX%2A><br /><br /> 默认值：0.0|<xref:System.Windows.Media.Matrix.OffsetY%2A><br /><br /> 默认值：0.0|1.0|  
  
 通过处理矩阵值，您可以旋转、按比例缩放、扭曲和移动（平移）对象。  例如，如果将第三行第一列中的值（<xref:System.Windows.Media.Matrix.OffsetX%2A> 值）更改为 100，则可以使用它将对象沿 x 轴移动 100 个单位。  如果将第二行第二列中的值更改为 3，您可以使用它将对象拉伸为其当前高度的三倍。  如果同时更改两个值，则可将对象沿 x 轴移动 100 个单位并将其高度拉伸 3 倍。  由于 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 仅支持仿射变换，因此右边列中的值始终为 0、0、1。  
  
 尽管 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 使您能够直接处理矩阵值，但它还提供了许多 <xref:System.Windows.Media.Transform> 类，您可以使用这些类来变换对象，而无需了解基础矩阵结构的配置方式。  例如，利用 <xref:System.Windows.Media.ScaleTransform> 类，您可以通过设置对象的 <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 和 <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> 属性来按比例缩放对象，而不用处理变换矩阵。  同样，利用 <xref:System.Windows.Media.RotateTransform> 类，您只需通过设置对象的 <xref:System.Windows.Media.RotateTransform.Angle%2A> 属性即可旋转对象。  
  
<a name="transformClassesSection"></a>   
## 变换类  
 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 为常见变换操作提供了以下 [!INCLUDE[TLA#tla_2d](../../../../includes/tlasharptla-2d-md.md)] <xref:System.Windows.Media.Transform> 类：  
  
|类|说明|示例|图示|  
|-------|--------|--------|--------|  
|<xref:System.Windows.Media.RotateTransform>|按指定的 <xref:System.Windows.Media.RotateTransform.Angle%2A> 旋转元素。|[旋转对象](../../../../docs/framework/wpf/graphics-multimedia/how-to-rotate-an-object.md)||  
|<xref:System.Windows.Media.ScaleTransform>|按指定的 <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 和 <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> 量按比例缩放元素。|[缩放元素](../../../../docs/framework/wpf/graphics-multimedia/how-to-scale-an-element.md)||  
|<xref:System.Windows.Media.SkewTransform>|按指定的 <xref:System.Windows.Media.SkewTransform.AngleX%2A> 和 <xref:System.Windows.Media.SkewTransform.AngleY%2A> 量扭曲元素。|[使元素扭曲](../../../../docs/framework/wpf/graphics-multimedia/how-to-skew-an-element.md)||  
|<xref:System.Windows.Media.TranslateTransform>|按指定的 <xref:System.Windows.Media.TranslateTransform.X%2A> 和 <xref:System.Windows.Media.TranslateTransform.Y%2A> 量移动（平移）元素。|[平移元素](../../../../docs/framework/wpf/graphics-multimedia/how-to-translate-an-element.md)||  
  
 为了创建更复杂的变换，[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 提供了如下两个类：  
  
|类|说明|示例|  
|-------|--------|--------|  
|<xref:System.Windows.Media.TransformGroup>|将多个 <xref:System.Windows.Media.TransformGroup> 对象组合为可以随后应用于变换属性的单一 <xref:System.Windows.Media.Transform>。|[向对象应用多个变换](../../../../docs/framework/wpf/graphics-multimedia/how-to-apply-multiple-transforms-to-an-object.md)|  
|<xref:System.Windows.Media.MatrixTransform>|创建其他 <xref:System.Windows.Media.Transform> 类未提供的自定义变换。  在使用 <xref:System.Windows.Media.MatrixTransform> 时，将直接处理矩阵。|[使用 MatrixTransform 创建自定义变换](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-a-matrixtransform-to-create-custom-transforms.md)|  
  
 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 也提供[!INCLUDE[TLA#tla_3d](../../../../includes/tlasharptla-3d-md.md)]变换。  有关更多信息，请参见 <xref:System.Windows.Media.Media3D.Transform3D> 类。  
  
<a name="transformationproperties"></a>   
## 常见变换属性  
 变换对象的一种方法是声明适当的 <xref:System.Windows.Media.Transform> 类型，并将其应用于对象的变换属性。  不同类型的对象具有不同类型的变换属性。  下表列出了若干常用的 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 类型及其变换属性。  
  
|类型|变换属性|  
|--------|----------|  
|<xref:System.Windows.Media.Brush>|<xref:System.Windows.Media.Brush.Transform%2A>, <xref:System.Windows.Media.Brush.RelativeTransform%2A>|  
|<xref:System.Windows.Media.ContainerVisual>|<xref:System.Windows.Media.ContainerVisual.Transform%2A>|  
|<xref:System.Windows.Media.DrawingGroup>|<xref:System.Windows.Media.DrawingGroup.Transform%2A>|  
|<xref:System.Windows.FrameworkElement>|<xref:System.Windows.UIElement.RenderTransform%2A>, <xref:System.Windows.FrameworkElement.LayoutTransform%2A>|  
|<xref:System.Windows.Media.Geometry>|<xref:System.Windows.Media.Geometry.Transform%2A>|  
|<xref:System.Windows.Media.TextEffect>|<xref:System.Windows.Media.TextEffect.Transform%2A>|  
|<xref:System.Windows.UIElement>|<xref:System.Windows.UIElement.RenderTransform%2A>|  
  
<a name="transformcenter"></a>   
## 变换和坐标系  
 在变换对象时，您不仅仅是变换对象，您变换的是对象所在的坐标系。  默认情况下，变换将以目标对象坐标系的原点 \(0,0\) 为中心进行。  唯一的例外是 <xref:System.Windows.Media.TranslateTransform>；<xref:System.Windows.Media.TranslateTransform> 没有要设置的中心属性，因为不管以何处为中心，平移效果都相同。  
  
 下面的示例使用 <xref:System.Windows.Media.RotateTransform>，围绕其默认中心 \(0, 0\) 将 <xref:System.Windows.Shapes.Rectangle> 元素（一种 <xref:System.Windows.FrameworkElement>）旋转 45 度。  下图显示了旋转的效果。  
  
 ![围绕 &#40;0,0&#41; 旋转 45 度的 FrameworkElement](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-fe-rotated-about-upperleft-corner.png "graphicsmm\_FE\_rotated\_about\_upperleft\_corner")  
围绕点 \(0,0\) 旋转 45 度的矩形元素  
  
 [!code-xml[Transforms_snip#TransformsFERotatedAboutTopLeft](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/CoordinateSystemExample.xaml#transformsferotatedabouttopleft)]  
  
 默认情况下，元素将围绕其左上角 \(0, 0\) 旋转。  <xref:System.Windows.Media.RotateTransform>、<xref:System.Windows.Media.ScaleTransform> 和 <xref:System.Windows.Media.SkewTransform> 类提供 CenterX 和 CenterY 属性，可以利用这些属性来指定变换的应用点。  
  
 下一个示例也使用 <xref:System.Windows.Media.RotateTransform> 将 <xref:System.Windows.Shapes.Rectangle> 元素旋转 45 度；但是，这一次设置了 <xref:System.Windows.Media.RotateTransform.CenterX%2A> 和 <xref:System.Windows.Media.RotateTransform.CenterY%2A> 属性，因此 <xref:System.Windows.Media.RotateTransform> 的中心为 \(25, 25\)。  下图显示了旋转的效果。  
  
 ![围绕 &#40;25, 25&#41; 旋转 45 度的几何图形](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-fe-rotated-about-center.png "graphicsmm\_FE\_rotated\_about\_center")  
围绕点 \(25, 25\) 旋转 45 度的矩形元素  
  
 [!code-xml[Transforms_snip#TransformsFERotatedAboutCenter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/CoordinateSystemExample.xaml#transformsferotatedaboutcenter)]  
  
<a name="layoutTransformsAndRenderTransformsSection"></a>   
## 变换 FrameworkElement  
 若要将变换应用于 <xref:System.Windows.FrameworkElement>，请创建 <xref:System.Windows.Media.Transform> 并将其应用于 <xref:System.Windows.FrameworkElement> 类提供的两个属性之一：  
  
-   <xref:System.Windows.FrameworkElement.LayoutTransform%2A> — 在布局处理过程之前应用的变换。  应用了变换后，布局系统将处理元素的变换后大小和位置。  
  
-   <xref:System.Windows.UIElement.RenderTransform%2A> — 修改元素的外观但在布局处理过程完成之后应用的变换。  通过使用 <xref:System.Windows.UIElement.RenderTransform%2A> 属性（而不是 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 属性），您可以使性能得到优化。  
  
 应使用哪个属性？  由于 <xref:System.Windows.UIElement.RenderTransform%2A> 属性能够使性能得到优化，因此请尽可能使用该属性，特别是在使用带有动画效果的 <xref:System.Windows.Media.Transform> 对象时。  在按比例缩放、旋转或扭曲时使用 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 属性，并且，您需要元素的父项适应元素的变换后大小。  请注意，将 <xref:System.Windows.Media.TranslateTransform> 对象与 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 属性一起使用时，这些对象似乎对元素没有影响。  这是因为布局系统在处理过程中会使平移的元素回到其原始位置。  
  
 有关 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的布局的附加信息，请参见[布局](../../../../docs/framework/wpf/advanced/layout.md)概述。  
  
<a name="exampleRotateAnElement45degSection"></a>   
## 示例：将 FrameworkElement 旋转 45 度  
 下面的示例使用 <xref:System.Windows.Media.RotateTransform> 将按钮沿顺时针方向旋转 45 度。  该按钮包含在具有两个其他按钮的 <xref:System.Windows.Controls.StackPanel> 中。  
  
 默认情况下，<xref:System.Windows.Media.RotateTransform> 围绕点 \(0, 0\) 旋转。  由于示例未指定中心值，因此按钮将围绕点 \(0, 0\)（即按钮的左上角）旋转。  <xref:System.Windows.Media.RotateTransform> 应用于 <xref:System.Windows.UIElement.RenderTransform%2A> 属性。  下图显示了变换的效果。  
  
 ![使用 RenderTransform 变换的按钮](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rendertransformwithdefaultcenter.png "graphicsmm\_RenderTransformWithDefaultCenter")  
从左上角沿顺时针方向旋转 45 度  
  
 [!code-xml[Transforms_snip#GraphicsMMRotateButtonExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample1)]  
  
 下一个示例也使用 <xref:System.Windows.Media.RotateTransform> 将按钮沿顺时针方向旋转 45 度，但它同时将按钮的 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 设置为 \(0.5, 0.5\)。  <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 属性的值与按钮的大小相关。  因此，将在按钮的中心（而不是其左上角）应用旋转。  下图显示了变换的效果。  
  
 ![围绕中心变换的按钮](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rendertransformrelativecenter.png "graphicsmm\_RenderTransformRelativeCenter")  
围绕中心沿顺时针方向旋转 45 度  
  
 [!code-xml[Transforms_snip#GraphicsMMRotateButtonExample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample2)]  
  
 下面的示例使用 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 属性（而不是 <xref:System.Windows.UIElement.RenderTransform%2A> 属性）来旋转按钮。  这样会使变换影响按钮的布局，从而触发布局系统的全面处理过程。  因此，将会旋转按钮，然后重新定位按钮，因为按钮大小发生了变化。  下图显示了变换的效果。  
  
 ![使用 LayoutTransform 变换的按钮](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-layouttransform.png "graphicsmm\_LayoutTransform")  
用于旋转按钮的 LayoutTransform  
  
 [!code-xml[Transforms_snip#GraphicsMMRotateButtonExample3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample3)]  
  
<a name="animate_transforms"></a>   
## 对变换进行动画处理  
 由于 <xref:System.Windows.Media.Transform> 类继承自 <xref:System.Windows.Media.Animation.Animatable> 类，因此可以对它们进行动画处理。  若要对 <xref:System.Windows.Media.Transform> 进行动画处理，请将类型兼容的动画应用于想要进行动画处理的属性。  
  
 下面的示例将 <xref:System.Windows.Media.Animation.Storyboard> 和 <xref:System.Windows.Media.Animation.DoubleAnimation> 与 <xref:System.Windows.Media.RotateTransform> 一起使用，以便在单击 <xref:System.Windows.Controls.Button> 时使其旋转到位。  
  
 [!code-xml[Transforms_snip#GraphicsMMAnimatedRotateButtonExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonAnimatedRotateTransformExample.xaml#graphicsmmanimatedrotatebuttonexamplewholepage)]  
  
 有关完整示例，请参见 [2\-D Transforms Sample](http://go.microsoft.com/fwlink/?LinkID=158252)（二维转换示例）。  有关动画的更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
<a name="freezable_features"></a>   
## Freezable 功能  
 由于 <xref:System.Windows.Media.Transform> 类继承自 <xref:System.Windows.Freezable> 类，因此它提供了多种特殊功能：<xref:System.Windows.Media.Transform> 对象可声明为[资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)、在多个对象之间共享、设为只读以提高性能、进行克隆以及设为线程安全。  有关 <xref:System.Windows.Freezable> 对象提供的不同功能的更多信息，请参见[Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.Transform>   
 <xref:System.Windows.Media.Matrix>   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)   
 [2\-D Transforms Sample](http://go.microsoft.com/fwlink/?LinkID=158252)