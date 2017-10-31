---
title: "如何：编码和解码 PNG 图像 | Microsoft Docs"
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
  - "解码 PNG 图像"
  - "编码图像格式"
  - "编码 PNG 图像"
  - "PNG 解码"
  - "PNG 编码"
ms.assetid: 3d31d186-af73-47f0-b5a7-c26ae46409a6
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：编码和解码 PNG 图像
下面的示例演示如何使用特定的 <xref:System.Windows.Media.Imaging.PngBitmapDecoder> 和 <xref:System.Windows.Media.Imaging.PngBitmapEncoder> 对象来对[!INCLUDE[TLA#tla_png](../../../../includes/tlasharptla-png-md.md)] 图像进行解码和编码。  
  
## 示例  
 此示例演示如何使用 <xref:System.IO.FileStream> 中的 <xref:System.Windows.Media.Imaging.PngBitmapDecoder> 对[!INCLUDE[TLA2#tla_png](../../../../includes/tla2sharptla-png-md.md)] 图像进行解码。  
  
 [!code-cpp[PngBitmapDecoderEncoder#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CPP/PngEncoderDecoder.cpp#1)]
 [!code-csharp[PngBitmapDecoderEncoder#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CSharp/PngEncoderDecoder.cs#1)]
 [!code-vb[PngBitmapDecoderEncoder#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PngBitmapDecoderEncoder/VB/PngEncoderDecoder.vb#1)]  
  
## 示例  
 本示例演示如何使用 <xref:System.Windows.Media.Imaging.PngBitmapEncoder> 将 <xref:System.Windows.Media.Imaging.BitmapSource> 编码为 [!INCLUDE[TLA2#tla_png](../../../../includes/tla2sharptla-png-md.md)] 图像。  
  
 [!code-cpp[PngBitmapDecoderEncoder#4](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CPP/PngEncoderDecoder.cpp#4)]
 [!code-csharp[PngBitmapDecoderEncoder#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CSharp/PngEncoderDecoder.cs#4)]
 [!code-vb[PngBitmapDecoderEncoder#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PngBitmapDecoderEncoder/VB/PngEncoderDecoder.vb#4)]  
  
## 请参阅  
 [图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)