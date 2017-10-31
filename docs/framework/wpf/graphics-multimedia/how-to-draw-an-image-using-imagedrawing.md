---
title: "如何：使用 ImageDrawing 绘制图像 | Microsoft Docs"
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
  - "类, ImageDrawing"
  - "绘图, 图像"
  - "图形, 绘制图像"
  - "ImageDrawing 类"
  - "图像, 绘图"
ms.assetid: df28ab41-25fb-4ab3-b51d-7f695b24f55e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使用 ImageDrawing 绘制图像
本示例演示如何使用 <xref:System.Windows.Media.ImageDrawing> 来绘制图像。  使用 <xref:System.Windows.Media.ImageDrawing>，可以借助于 <xref:System.Windows.Media.DrawingBrush>、<xref:System.Windows.Media.DrawingImage> 或 <xref:System.Windows.Media.Visual> 来显示 <xref:System.Windows.Media.ImageSource>。  若要绘制图像，请创建一个 <xref:System.Windows.Media.ImageDrawing> 并设置它的 <xref:System.Windows.Media.ImageDrawing.ImageSource%2A?displayProperty=fullName> 和 <xref:System.Windows.Media.ImageDrawing.Rect%2A?displayProperty=fullName> 属性。  <xref:System.Windows.Media.ImageDrawing.ImageSource%2A?displayProperty=fullName> 属性指定要绘制的图像，<xref:System.Windows.Media.ImageDrawing.Rect%2A?displayProperty=fullName> 属性指定每个图像的位置和大小。  
  
## 示例  
 下面的示例使用四个 <xref:System.Windows.Media.ImageDrawing> 对象创建一个复合绘图。  该示例生成下面的图像：  
  
 ![几个 DrawingImage 对象](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-imagedrawingexample.png "graphicsmm\_ImageDrawingExample")  
四个 ImageDrawing 对象  
  
 [!code-csharp[DrawingMiscSnippets_snip#ImageDrawingExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/ImageDrawingExample.cs#imagedrawingexample)]
 [!code-xml[DrawingMiscSnippets_snip#ImageDrawingExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/ImageDrawingExample.xaml#imagedrawingexample)]  
  
 有关演示在不使用 <xref:System.Windows.Media.ImageDrawing> 的情况下显示图像的简单方法的示例，请参见[使用 Image 元素](../../../../docs/framework/wpf/controls/how-to-use-the-image-element.md)。  
  
## 请参阅  
 <xref:System.Windows.Freezable.Freeze%2A>   
 <xref:System.Windows.Controls.Image>   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [PresentationOptions:Freeze 特性](../../../../docs/framework/wpf/advanced/presentationoptions-freeze-attribute.md)