---
title: "如何：使用 TileBrush 创建不同的平铺模式 | Microsoft Docs"
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
  - "创建, 使用 TileBrush 创建平铺模式"
  - "平铺模式, 创建"
  - "TileBrush, 创建平铺模式"
ms.assetid: 5aa46632-3527-4668-9d8d-0375c8af28aa
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用 TileBrush 创建不同的平铺模式
本示例演示如何使用 <xref:System.Windows.Media.TileBrush> 的 <xref:System.Windows.Media.TileBrush.TileMode%2A> 属性创建图案。  
  
 通过 <xref:System.Windows.Media.TileBrush.TileMode%2A> 属性可以指定如何重复 <xref:System.Windows.Media.TileBrush> 的内容，即，如何平铺图块内容以填充输出区域。  若要创建图案，请将 <xref:System.Windows.Media.TileBrush.TileMode%2A> 设置为 <xref:System.Windows.Media.TileMode>、<xref:System.Windows.Media.TileMode>、<xref:System.Windows.Media.TileMode> 或 <xref:System.Windows.Media.TileMode>。  还必须设置 <xref:System.Windows.Media.TileBrush> 的<xref:System.Windows.Media.TileBrush.Viewport%2A>，使其小于您正在绘制的区域；否则，无论您使用哪个 <xref:System.Windows.Media.TileBrush.TileMode%2A> 设置，都只能生成一个图块。  
  
## 示例  
 下面的示例创建五个 <xref:System.Windows.Media.DrawingBrush> 对象，每个对象具有不同的 <xref:System.Windows.Media.TileBrush.TileMode%2A> 设置，并使用它们绘制五个矩形。  尽管此示例使用 <xref:System.Windows.Media.DrawingBrush> 类来演示 <xref:System.Windows.Media.TileBrush.TileMode%2A> 的行为，但是 <xref:System.Windows.Media.TileBrush.TileMode%2A> 属性对于所有 <xref:System.Windows.Media.TileBrush> 对象（即 <xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.VisualBrush> 和 <xref:System.Windows.Media.DrawingBrush>）的工作方式都相同。  
  
 下面的插图演示此示例生成的输出。  
  
 ![TileBrush 平铺示例输出](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-drawingbrushtilemodeexample.png "graphicsmm\_DrawingBrushTileModeExample")  
使用 TileMode 属性创建的图块图案  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/TileModeExample.cs#graphicsmmdrawingbrushtilemodeexample)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/tilemodeexample.vb#graphicsmmdrawingbrushtilemodeexample)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/TileModeExample.xaml#graphicsmmdrawingbrushtilemodeexample)]  
  
## 请参阅  
 [为 TileBrush 设置平铺大小](../../../../docs/framework/wpf/graphics-multimedia/how-to-set-the-tile-size-for-a-tilebrush.md)   
 [使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)