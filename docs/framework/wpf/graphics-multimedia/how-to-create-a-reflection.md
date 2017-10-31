---
title: "如何：创建反射 | Microsoft Docs"
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
  - "画笔, 创建反射"
  - "创建反射"
  - "反射, 创建"
ms.assetid: 4f017e16-ab80-43c7-98df-03b6bddbb203
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：创建反射
本示例演示如何使用 <xref:System.Windows.Media.VisualBrush> 创建反射。  由于 <xref:System.Windows.Media.VisualBrush> 可以显示现有可视项目，您可以使用此功能生成有趣的可视效果，例如反射和放大。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.VisualBrush> 创建包含若干元素的 <xref:System.Windows.Controls.Border> 的反射。  下面的插图演示此示例生成的输出。  
  
 ![反射的 Visual 对象](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-visualbrush-reflection-small.png "graphicsmm\_visualbrush\_reflection\_small")  
反射的 Visual 对象  
  
 [!code-csharp[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/ReflectionExample.cs#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-vb[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/reflectionexample.vb#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-xml[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/ReflectionExample.xaml#graphicsmmvisualbrushreflectionexamplewholepage)]  
  
 有关完整示例，其中包括如何放大屏幕的各部分以及如何创建反射的示例，请参见 [VisualBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160049)（VisualBrush 示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.VisualBrush>   
 [使用图像、绘图和 Visual 进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)