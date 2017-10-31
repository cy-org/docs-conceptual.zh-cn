---
title: "如何：将 Visual 编码为图像文件 | Microsoft Docs"
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
  - "编码图像格式"
  - "图像文件, 从可视化效果编码"
  - "视觉效果, 编码到图像文件"
ms.assetid: 2036385b-ea47-4d54-8027-5797f52c8149
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：将 Visual 编码为图像文件
本示例演示如何使用 <xref:System.Windows.Media.Imaging.RenderTargetBitmap> 和 <xref:System.Windows.Media.Imaging.PngBitmapEncoder> 将 <xref:System.Windows.Media.Visual> 对象编码为图像文件。  
  
## 示例  
 <xref:System.Windows.Media.DrawingVisual> 是使用 <xref:System.Windows.Media.Imaging.BitmapImage> 和 <xref:System.Windows.Media.FormattedText> 创建的，后者呈现到 <xref:System.Windows.Media.Imaging.RenderTargetBitmap> 上。  然后使用呈现的位图创建 <xref:System.Windows.Media.Imaging.BitmapFrame>，它将添加到 <xref:System.Windows.Media.Imaging.PngBitmapEncoder> 以创建一个新的[!INCLUDE[TLA#tla_png](../../../../includes/tlasharptla-png-md.md)] 文件。  
  
 [!code-csharp[ImagingSnippetGallery_procedural_snip#RTBEncodeInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/CSharp/RenderTargetBitmapExample_Encode.cs#rtbencodeinline1)]
 [!code-vb[ImagingSnippetGallery_procedural_snip#RTBEncodeInline1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/VB/RenderTargetBitmapExample_Encode.vb#rtbencodeinline1)]  
  
 本示例中使用了 <xref:System.Windows.Media.Imaging.PngBitmapEncoder>，但可以使用任何派生的 <xref:System.Windows.Media.Imaging.BitmapEncoder> 对象来创建图像文件。  
  
## 请参阅  
 <xref:System.Windows.Media.DrawingContext>   
 [图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [使用 DrawingVisual 对象](../../../../docs/framework/wpf/graphics-multimedia/using-drawingvisual-objects.md)