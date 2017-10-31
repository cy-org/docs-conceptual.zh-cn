---
title: "如何：编码和解码 GIF 图像 | Microsoft Docs"
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
  - "解码 GIF 图像"
  - "解码图像格式"
  - "编码 GIF 图像"
  - "编码图像格式"
  - "GIF 解码"
  - "GIF 编码"
ms.assetid: 9cdd9ec7-71eb-444b-b9e3-991958461163
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：编码和解码 GIF 图像
下面的示例演示如何使用特定的 <xref:System.Windows.Media.Imaging.GifBitmapDecoder> 和 <xref:System.Windows.Media.Imaging.GifBitmapEncoder> 对象来对[!INCLUDE[TLA#tla_gif](../../../../includes/tlasharptla-gif-md.md)] 图像进行解码和编码。  
  
## 示例  
 此示例演示如何使用 <xref:System.IO.FileStream> 中的 <xref:System.Windows.Media.Imaging.GifBitmapDecoder> 对[!INCLUDE[TLA2#tla_gif](../../../../includes/tla2sharptla-gif-md.md)] 图像进行解码。  
  
 [!code-cpp[GifBitmapDecoderEncoder#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CPP/GifEncoderDecoder.cpp#1)]
 [!code-csharp[GifBitmapDecoderEncoder#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CSharp/GifEncoderDecoder.cs#1)]
 [!code-vb[GifBitmapDecoderEncoder#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GifBitmapDecoderEncoder/VB/GifEncoderDecoder.vb#1)]  
  
## 示例  
 下面的示例演示如何使用 <xref:System.Windows.Media.Imaging.GifBitmapEncoder> 将 <xref:System.Windows.Media.Imaging.BitmapSource> 编码为 [!INCLUDE[TLA2#tla_gif](../../../../includes/tla2sharptla-gif-md.md)] 图像。  
  
 [!code-cpp[GifBitmapDecoderEncoder#4](../../../../samples/snippets/cpp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CPP/GifEncoderDecoder.cpp#4)]
 [!code-csharp[GifBitmapDecoderEncoder#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CSharp/GifEncoderDecoder.cs#4)]
 [!code-vb[GifBitmapDecoderEncoder#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GifBitmapDecoderEncoder/VB/GifEncoderDecoder.vb#4)]  
  
## 请参阅  
 [图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)