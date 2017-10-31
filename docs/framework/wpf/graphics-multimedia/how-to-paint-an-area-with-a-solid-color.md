---
title: "如何：使用纯色绘制区域 | Microsoft Docs"
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
  - "画笔, 使用纯色进行绘制"
  - "绘制, 使用纯色"
  - "纯色, 绘制"
ms.assetid: 5d27d8a7-4bd7-4063-bdf3-2c5c0f19f9d3
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用纯色绘制区域
若要使用纯色绘制区域，可以使用预定义的系统画笔，如 <xref:System.Windows.Media.Brushes.Red%2A> 或 <xref:System.Windows.Media.Brushes.Blue%2A>，也可以创建一个新的 <xref:System.Windows.Media.SolidColorBrush>，并使用 Alpha、红、绿、蓝值描述其 <xref:System.Windows.Media.SolidColorBrush.Color%2A>。  在 XAML 中，您还可以使用十六进制表示法来利用纯色绘制区域。  
  
 下面的示例分别使用上述每种方法绘制一个蓝色的 <xref:System.Windows.Shapes.Rectangle>。  
  
## 示例  
 **使用预定义画笔**  
  
 在下面的示例中，使用预定义的画笔 <xref:System.Windows.Media.Brushes.Blue%2A> 绘制一个蓝色矩形。  
  
 [!code-xml[brushsamples_snip#_graphicsmm_PredefinedBrush1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/SolidColorBrushExample.xaml#_graphicsmm_predefinedbrush1)]  
  
 [!code-csharp[brushsamples_procedural_snip#_graphicsmm_PredefinedBrush1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/SolidColorBrushExample.cs#_graphicsmm_predefinedbrush1)]  
  
 **使用十六进制表示法**  
  
 下一个示例使用 8 位十六进制表示法绘制一个蓝色矩形。  
  
 [!code-xml[brushsamples_snip#_graphicsmm_HexNotation8Digit1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/SolidColorBrushExample.xaml#_graphicsmm_hexnotation8digit1)]  
  
 **使用 ARGB 值**  
  
 下一个示例创建一个 <xref:System.Windows.Media.SolidColorBrush> 并使用蓝色的 ARGB 值描述其 <xref:System.Windows.Media.SolidColorBrush.Color%2A>。  
  
 [!code-xml[brushsamples_snip#_graphicsmm_RgbNotation1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/SolidColorBrushExample.xaml#_graphicsmm_rgbnotation1)]  
  
 [!code-csharp[brushsamples_procedural_snip#_graphicsmm_RgbNotation1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/SolidColorBrushExample.cs#_graphicsmm_rgbnotation1)]  
  
 有关描述颜色的其他方法，请参见 <xref:System.Windows.Media.Color> 结构。  
  
 **相关主题**  
  
 有关 <xref:System.Windows.Media.SolidColorBrush> 的更多信息以及其他示例，请参见[使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)概述。  
  
 此代码示例摘自一个为 <xref:System.Windows.Media.SolidColorBrush> 类提供的更大示例。  有关完整示例，请参见 [Brushes Sample](http://go.microsoft.com/fwlink/?LinkID=159973)（Brushes 示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.Brushes>