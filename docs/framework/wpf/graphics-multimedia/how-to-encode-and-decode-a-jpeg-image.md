---
title: "如何：编码和解码 JPEG 图像 | Microsoft Docs"
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
  - "解码图像格式"
  - "解码 JPEG 图像"
  - "编码图像格式"
  - "编码 JPEG 图像"
  - "JPEG 解码"
  - "JPEG 编码"
ms.assetid: b8cfde37-9f68-4911-a05e-51d8d7bdec7b
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：编码和解码 JPEG 图像
下面的示例演示如何使用特定的 <xref:System.Windows.Media.Imaging.JpegBitmapDecoder> 和 <xref:System.Windows.Media.Imaging.JpegBitmapEncoder> 对象来对 [!INCLUDE[TLA#tla_jpeg](../../../../includes/tlasharptla-jpeg-md.md)]图像进行解码和编码。  
  
## 示例  
 此示例演示如何使用 <xref:System.IO.FileStream> 中的 <xref:System.Windows.Media.Imaging.JpegBitmapDecoder> 对[!INCLUDE[TLA2#tla_jpeg](../../../../includes/tla2sharptla-jpeg-md.md)] 图像进行解码。  
  
 [!code-cpp[JpegBitmapDecoderEncoder#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/JpegBitmapDecoderEncoder/CPP/jpegencoderdecoder.cpp#1)]
 [!code-csharp[JpegBitmapDecoderEncoder#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/JpegBitmapDecoderEncoder/CSharp/JpegEncoderDecoder.cs#1)]
 [!code-vb[JpegBitmapDecoderEncoder#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/JpegBitmapDecoderEncoder/VB/JpegEncoderDecoder.vb#1)]  
  
## 示例  
 下面的示例演示如何使用 <xref:System.Windows.Media.Imaging.JpegBitmapEncoder> 将 <xref:System.Windows.Media.Imaging.BitmapSource> 编码为 [!INCLUDE[TLA2#tla_jpeg](../../../../includes/tla2sharptla-jpeg-md.md)] 图像。  
  
 [!code-cpp[JpegBitmapDecoderEncoder#4](../../../../samples/snippets/cpp/VS_Snippets_Wpf/JpegBitmapDecoderEncoder/CPP/jpegencoderdecoder.cpp#4)]
 [!code-csharp[JpegBitmapDecoderEncoder#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/JpegBitmapDecoderEncoder/CSharp/JpegEncoderDecoder.cs#4)]
 [!code-vb[JpegBitmapDecoderEncoder#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/JpegBitmapDecoderEncoder/VB/JpegEncoderDecoder.vb#4)]  
  
## .NET Framework 安全性  
  
## 请参阅  
 [图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)