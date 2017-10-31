---
title: "如何：将绘图用作图像源 | Microsoft Docs"
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
  - "绘图, 作为图像资源"
  - "图形, 绘图, 作为图像资源"
  - "图像资源, 绘图"
ms.assetid: dcf71c7b-9e86-4b8e-8e39-0d0ce0389ef4
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：将绘图用作图像源
本示例演示如何将 <xref:System.Windows.Media.Drawing> 用作 <xref:System.Windows.Controls.Image> 控件的 <xref:System.Windows.Controls.Image.Source%2A>。  若要使用 <xref:System.Windows.Controls.Image> 控件来显示 <xref:System.Windows.Media.Drawing>，请将 <xref:System.Windows.Media.DrawingImage> 用作 <xref:System.Windows.Controls.Image> 控件的 <xref:System.Windows.Controls.Image.Source%2A>，并将 <xref:System.Windows.Media.DrawingImage> 对象的 <xref:System.Windows.Media.DrawingImage.Drawing%2A?displayProperty=fullName> 属性设置为要显示的绘图。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.DrawingImage> 和 <xref:System.Windows.Controls.Image> 控件显示 <xref:System.Windows.Media.GeometryDrawing>。  该示例产生下面的输出：  
  
 ![两个椭圆的 GeometryDrawing](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-geodraw.png "graphicsmm\_geodraw")  
DrawingImage  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingImageExample.cs#drawingimageexamplewholepage)]
 [!code-xml[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingImageExample.xaml#drawingimageexamplewholepage)]  
  
## 请参阅  
 <xref:System.Windows.Freezable.Freeze%2A>   
 [使用 ImageDrawing 绘制图像](../../../../docs/framework/wpf/graphics-multimedia/how-to-draw-an-image-using-imagedrawing.md)   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [PresentationOptions:Freeze 特性](../../../../docs/framework/wpf/advanced/presentationoptions-freeze-attribute.md)