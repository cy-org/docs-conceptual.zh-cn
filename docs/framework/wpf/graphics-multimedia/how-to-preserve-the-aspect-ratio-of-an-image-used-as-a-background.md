---
title: "如何：保持背景图像的长宽比 | Microsoft Docs"
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
  - "背景图像的长宽比, 保留"
  - "背景图像, 保留长宽比"
  - "画笔, 保留背景图像的长宽比"
ms.assetid: 28c39478-13d7-4011-80a3-8b9cc3e54478
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：保持背景图像的长宽比
下面的示例演示如何使用 <xref:System.Windows.Media.ImageBrush> 的 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性来保持图像的[纵横比](GTMT)。  
  
 默认情况下，当您使用 <xref:System.Windows.Media.ImageBrush> 绘制某个区域时，该区域的内容将进行拉伸以完全填充输出区域。  当输出区域和图像的[纵横比](GTMT)不同时，图像就会因拉伸而失真。  
  
 为了让 <xref:System.Windows.Media.ImageBrush> 保持其图像的长宽比，请将 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性设置为 <xref:System.Windows.Media.Stretch> 或 <xref:System.Windows.Media.Stretch>。  
  
## 示例  
 下面的示例使用两个 <xref:System.Windows.Media.ImageBrush> 对象来绘制两个矩形。  每个矩形都为 300x150 [像素](GTMT)，每个矩形都包含一个 300x 300 像素的图像。  第一个画笔的 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性设置为 <xref:System.Windows.Media.Stretch>，第二个画笔的 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性设置为 <xref:System.Windows.Media.Stretch>。  
  
 [!code-csharp[UsingImageBrush_snip#ImageBrushStretchModesExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/StretchModes.cs#imagebrushstretchmodesexamplewholepage)]  
  
 下面的插图显示第一个画笔的输出，该画笔的 <xref:System.Windows.Media.TileBrush.Stretch%2A> 设置为 <xref:System.Windows.Media.Stretch>。  
  
 ![具有 Uniform 拉伸的 ImageBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-imagebrushuniformstretch.png "graphicsmm\_ImageBrushUniformStretch")  
  
 下一个插图显示第二个画笔的输出，该画笔的 <xref:System.Windows.Media.TileBrush.Stretch%2A> 设置为 <xref:System.Windows.Media.Stretch>。  
  
 ![具有 UniformToFill 拉伸的 ImageBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-imagebrushuniformtofillstretch.png "graphicsmm\_ImageBrushUniformToFillStretch")  
  
 请注意，<xref:System.Windows.Media.TileBrush.Stretch%2A> 属性对于其他 <xref:System.Windows.Media.TileBrush> 对象（即，<xref:System.Windows.Media.DrawingBrush> 和 <xref:System.Windows.Media.VisualBrush>）的行为方式相同。  有关 <xref:System.Windows.Media.ImageBrush> 和其他 <xref:System.Windows.Media.TileBrush> 对象的更多信息，请参见[使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)。  
  
 另请注意，尽管 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性似乎指定 <xref:System.Windows.Media.TileBrush> 内容如何拉伸以适合其输出区域，但是它实际上指定 <xref:System.Windows.Media.TileBrush> 内容如何拉伸以填充其基本平铺图像。  有关更多信息，请参见 <xref:System.Windows.Media.TileBrush>。  
  
 此代码示例摘自一个为 <xref:System.Windows.Media.ImageBrush> 类提供的更大的示例。  有关完整示例，请参见 [ImageBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160005)（ImageBrush 示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.TileBrush>   
 [使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)