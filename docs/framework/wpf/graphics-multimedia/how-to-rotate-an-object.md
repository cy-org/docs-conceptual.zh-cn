---
title: "如何：旋转对象 | Microsoft Docs"
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
  - "图形, 旋转对象"
  - "旋转对象"
ms.assetid: ee3466cd-e66f-4e8f-8a5a-71d77bc1e390
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：旋转对象
此示例演示如何旋转对象。  此示例首先创建一个 <xref:System.Windows.Media.RotateTransform>，然后以角度为单位指定了其 <xref:System.Windows.Media.RotateTransform.Angle%2A>。  
  
 下面的示例以 <xref:System.Windows.Shapes.Polyline> 对象的左上角为旋转点将其旋转了 45 度。  
  
## 示例  
 [!code-xml[Transforms_snip#RotatePolylineAboutTopLeft](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/RotateTransformExample.xaml#rotatepolylineabouttopleft)]  
  
 [!code-csharp[Transforms_Procedural_snip#RotatePolylineAboutTopLeft](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/RotateTransformExample.cs#rotatepolylineabouttopleft)]
 [!code-vb[Transforms_Procedural_snip#RotatePolylineAboutTopLeft](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/RotateTransformExample.vb#rotatepolylineabouttopleft)]  
  
 <xref:System.Windows.Media.RotateTransform> 的 <xref:System.Windows.Media.RotateTransform.CenterX%2A> 和 <xref:System.Windows.Media.RotateTransform.CenterY%2A> 属性指定了对象的旋转点。  此中心点以变换的元素的坐标空间来表示。  默认情况下，将围绕着要变换的对象的左上角 \(0,0\) 进行旋转。  
  
 下一个示例围绕点 \(25,50\) 沿顺时针方向将 <xref:System.Windows.Shapes.Polyline> 对象旋转了 45 度。  
  
 [!code-xml[Transforms_snip#RotatePolylineAboutCenter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/RotateTransformExample.xaml#rotatepolylineaboutcenter)]  
  
 [!code-csharp[Transforms_Procedural_snip#RotatePolylineAboutCenter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/RotateTransformExample.cs#rotatepolylineaboutcenter)]
 [!code-vb[Transforms_Procedural_snip#RotatePolylineAboutCenter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/RotateTransformExample.vb#rotatepolylineaboutcenter)]  
  
 下图显示了对这两个对象应用 <xref:System.Windows.Media.Transform> 后的结果。  
  
 ![以不同中心点进行的 45 度旋转](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-rotatetransform45degrees.png "wcpsdk\_graphicsmm\_rotatetransform45degrees")  
两个对象从不同的旋转中心旋转了 45 度  
  
 前面示例中的 <xref:System.Windows.Shapes.Polyline> 是 <xref:System.Windows.UIElement>。  对 <xref:System.Windows.UIElement> 的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性应用 <xref:System.Windows.Media.Transform> 时，可以使用 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 属性指定对元素应用的每个 <xref:System.Windows.Media.Transform> 的原点。  因为 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 属性使用相对坐标，所以即使不知道元素的尺寸，也仍然可以对元素中心应用变换。  有关更多信息及示例，请参见[使用相对值指定变换原点](../../../../docs/framework/wpf/graphics-multimedia/how-to-specify-the-origin-of-a-transform-by-using-relative-values.md)。  
  
 有关完整示例，请参见 [2\-D Transforms Sample](http://go.microsoft.com/fwlink/?LinkID=158252)（二维转换示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.Transform>   
 [变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)