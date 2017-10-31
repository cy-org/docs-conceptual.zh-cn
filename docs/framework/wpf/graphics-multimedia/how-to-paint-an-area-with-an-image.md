---
title: "如何：使用图像绘制区域 | Microsoft Docs"
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
  - "画笔, 使用图像进行绘制"
  - "图像, 绘制"
  - "绘制, 使用图像"
ms.assetid: 3432c533-1fc7-492d-94ee-0b13d60125ae
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用图像绘制区域
此示例演示如何使用 <xref:System.Windows.Media.ImageBrush> 类来绘制带有图像的区域。  <xref:System.Windows.Media.ImageBrush> 显示由其 <xref:System.Windows.Media.ImageBrush.ImageSource%2A> 属性指定的单个图像。  
  
## 示例  
 下面的示例通过使用 <xref:System.Windows.Media.ImageBrush> 绘制按钮的 <xref:System.Windows.Controls.Control.Background%2A>。  
  
 [!code-csharp[UsingImageBrush_snip#ImageBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/PaintingWithImagesExample.cs#imagebrushexamplewholepage)]  
  
 默认情况下，<xref:System.Windows.Media.ImageBrush> 拉伸其图像以完全填充您绘制的区域。  在上面的示例中，拉伸图像以填充按钮，可能扭曲图像。  可以通过将 <xref:System.Windows.Media.TileBrush> 的 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性设置为 <xref:System.Windows.Media.Stretch> 或 <xref:System.Windows.Media.Stretch> 来控制此行为，这样会使画笔保留图像的[纵横比](GTMT)。  
  
 如果设置 <xref:System.Windows.Media.ImageBrush> 的 <xref:System.Windows.Media.TileBrush.Viewport%2A> 和 <xref:System.Windows.Media.TileBrush.TileMode%2A> 属性，则可以创建重复的图案。  下面的示例通过使用从图像创建的图案来绘制按钮。  
  
 [!code-csharp[UsingImageBrush_snip#TiledImageBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TiledImageBrushExample.cs#tiledimagebrushexamplewholepage)]
 [!code-vb[UsingImageBrush_snip#TiledImageBrushExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UsingImageBrush_snip/VisualBasic/TiledImageBrushExample.vb#tiledimagebrushexamplewholepage)]  
  
 有关 <xref:System.Windows.Media.ImageBrush> 类的更多信息，请参见[使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)。  
  
 此代码示例摘自一个为 <xref:System.Windows.Media.ImageBrush> 类提供的更大的示例。  有关完整示例，请参见 [ImageBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160005)（ImageBrush 示例）。  
  
## 请参阅  
 [使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)