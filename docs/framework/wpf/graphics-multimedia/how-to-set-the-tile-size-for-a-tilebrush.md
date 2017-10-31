---
title: "如何：为 TileBrush 设置平铺大小 | Microsoft Docs"
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
  - "TileBrush, 平铺大小"
  - "TileBrush 的视区属性"
ms.assetid: 04f41090-1b46-4e36-832f-d27d28708b8c
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：为 TileBrush 设置平铺大小
下面的示例演示如何为 <xref:System.Windows.Media.TileBrush> 设置图块大小。  默认情况下，<xref:System.Windows.Media.TileBrush> 生成一个可完全填充所绘制区域的图块。  可以通过设置 <xref:System.Windows.Media.TileBrush.Viewport%2A> 和 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 属性来重写此行为。  
  
 <xref:System.Windows.Media.TileBrush.Viewport%2A> 属性可以为 <xref:System.Windows.Media.TileBrush> 指定图块大小。  默认情况下，<xref:System.Windows.Media.TileBrush.Viewport%2A> 属性值相对于所绘制区域的大小。  为了让 <xref:System.Windows.Media.TileBrush.Viewport%2A> 属性指定绝对图块大小，请将 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 属性设置为 <xref:System.Windows.Media.BrushMappingMode>。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.ImageBrush>（<xref:System.Windows.Media.TileBrush> 的一个类型）来绘制带有图块的矩形。  此示例将每个图块图像设置为在长宽方向上分别占输出区域（矩形）的 50%。  因此，该矩形将用图块图像的四个投影来绘制。  
  
 下面的插图显示由该示例生成的输出。  
  
 ![使用图像画笔平铺的示例](../../../../docs/framework/wpf/graphics-multimedia/media/0.png "0")  
  
 [!code-csharp[UsingImageBrush_snip#RelativeTileSizeExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TileSizeExample.cs#relativetilesizeexample)]  
  
 下一个示例创建一个 <xref:System.Windows.Media.ImageBrush>，将它的 <xref:System.Windows.Media.TileBrush.Viewport%2A> 设置为 `0,0,25,25`，将它的 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 设置为 <xref:System.Windows.Media.BrushMappingMode>，并使用它来绘制另一个矩形。  因此，画笔会生成一个宽度为 25 [像素](GTMT)、高度为 25 [像素](GTMT)的图块。  
  
 下面的插图显示由该示例生成的输出。  
  
 ![一个平铺的 TileBrush，其视区为 0,0,0.25,0.25](../../../../docs/framework/wpf/graphics-multimedia/media/25x25viewport.png "25x25viewport")  
  
 [!code-csharp[UsingImageBrush_snip#AbsoluteTileSizeExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TileSizeExample.cs#absolutetilesizeexample)]  
  
 上面的几个示例摘自一个更大的示例。  有关完整示例，请参见 [ImageBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160005)（ImageBrush 示例）。  
  
 尽管此示例使用 <xref:System.Windows.Media.ImageBrush> 类，但是 <xref:System.Windows.Media.TileBrush.Viewport%2A> 和 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 属性对于其他 <xref:System.Windows.Media.TileBrush> 对象（即 <xref:System.Windows.Media.DrawingBrush> 和 <xref:System.Windows.Media.VisualBrush>）的行为方式是相同的。  有关 <xref:System.Windows.Media.ImageBrush> 和其他 <xref:System.Windows.Media.TileBrush> 对象的更多信息，请参见[使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.TileBrush>   
 [使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [使用 TileBrush 创建不同的平铺模式](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-different-tile-patterns-with-a-tilebrush.md)