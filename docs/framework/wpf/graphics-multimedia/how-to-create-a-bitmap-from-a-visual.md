---
title: "如何：从 Visual 创建位图 | Microsoft Docs"
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
  - "bitmaps, 从可视化效果呈现"
  - "视觉效果, 呈现到位图"
ms.assetid: 103fc7f5-7306-4026-9d61-2005e79959f3
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：从 Visual 创建位图
本示例演示如何从 <xref:System.Windows.Media.Visual> 创建位图。  <xref:System.Windows.Media.DrawingVisual> 是使用 <xref:System.Windows.Media.FormattedText> 呈现的。  <xref:System.Windows.Media.Visual> 然后呈现给 <xref:System.Windows.Media.Imaging.RenderTargetBitmap> 以创建给定文本的位图。  
  
## 示例  
 [!code-csharp[ImagingSnippetGallery_procedural_snip#CreateRTBImage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/CSharp/RenderTargetBitmapExample.cs#creatertbimage)]
 [!code-vb[ImagingSnippetGallery_procedural_snip#CreateRTBImage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/VB/RenderTargetBitmapExample.vb#creatertbimage)]  
  
## 请参阅  
 <xref:System.Windows.Media.DrawingContext>   
 [图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [使用 DrawingVisual 对象](../../../../docs/framework/wpf/graphics-multimedia/using-drawingvisual-objects.md)