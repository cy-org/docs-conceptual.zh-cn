---
title: "如何：变换画笔 | Microsoft Docs"
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
  - "画笔, 旋转内容"
  - "画笔, 变换属性"
  - "旋转画笔的内容"
ms.assetid: ebada2f9-f01f-4863-9ea2-c2e4e51610f1
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：变换画笔
此示例演示如何使用 <xref:System.Windows.Media.Brush> 对象的两个变换属性 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 和 <xref:System.Windows.Media.Brush.Transform%2A> 来变换这些对象。  
  
 下面的示例使用 <xref:System.Windows.Media.RotateTransform> 将 <xref:System.Windows.Media.ImageBrush> 的内容旋转 45 度。  
  
 下图显示了以下三种情况下的 <xref:System.Windows.Media.ImageBrush>：无 <xref:System.Windows.Media.RotateTransform>、对 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 属性应用了 <xref:System.Windows.Media.RotateTransform> 以及对 <xref:System.Windows.Media.Brush.Transform%2A> 属性应用了 <xref:System.Windows.Media.RotateTransform>。  
  
 ![画笔的 RelativeTransform 和 Transform 设置](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-transformandrelativetransform.png "wcpsdk\_graphicsmm\_transformandrelativetransform")  
  
## 示例  
 第一个示例将 <xref:System.Windows.Media.RotateTransform> 应用于 <xref:System.Windows.Media.ImageBrush> 的 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 属性。  <xref:System.Windows.Media.RotateTransform> 对象的 <xref:System.Windows.Media.RotateTransform.CenterX%2A> 和 <xref:System.Windows.Media.RotateTransform.CenterY%2A> 属性都被设置为 0.5，这是此内容的中心点的相对坐标。  因此，<xref:System.Windows.Media.ImageBrush> 内容将围绕其中心旋转。  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushrelativetransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushrelativetransformexample)]
 [!code-xml[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushrelativetransformexample)]  
  
 第二个示例也将 <xref:System.Windows.Media.RotateTransform> 应用于 <xref:System.Windows.Media.ImageBrush>；但是，此示例使用 <xref:System.Windows.Media.Brush.Transform%2A> 属性，而不是使用 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 属性。  
  
 为了使画笔围绕其中心旋转，此示例将 <xref:System.Windows.Media.RotateTransform> 对象的 <xref:System.Windows.Media.RotateTransform.CenterX%2A> 和 <xref:System.Windows.Media.RotateTransform.CenterY%2A> 属性设置为绝对坐标。  因为画笔绘制了一个 175 x 90 [像素](GTMT)的矩形，所以此矩形的中心点坐标为 \(87.5, 45\)。  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushTransformExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushtransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushTransformExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushtransformexample)]
 [!code-xml[BrushesIntroduction_snip#ImageBrushTransformExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushtransformexample)]  
  
 有关 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 和 <xref:System.Windows.Media.Brush.Transform%2A> 属性的工作原理的说明，请参见[Brush 变换概述](../../../../docs/framework/wpf/graphics-multimedia/brush-transformation-overview.md)。  
  
 有关完整示例，请参见 [Brushes Sample](http://go.microsoft.com/fwlink/?LinkID=159973)（Brushes 示例）。  有关画笔的更多信息，请参见[使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)。  
  
## 请参阅  
 [Brush 变换概述](../../../../docs/framework/wpf/graphics-multimedia/brush-transformation-overview.md)   
 [使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)