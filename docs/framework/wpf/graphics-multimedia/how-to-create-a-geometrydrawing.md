---
title: "如何：创建 GeometryDrawing | Microsoft Docs"
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
  - "类, GeometryDrawing"
  - "GeometryDrawing 类"
  - "图形, GeometryDrawing 类"
  - "可呈现的形状"
  - "形状, 可呈现的"
ms.assetid: 11d3c096-91ba-4d41-9bba-aeac0db70f97
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：创建 GeometryDrawing
本示例演示如何创建和显示 <xref:System.Windows.Media.GeometryDrawing>。  <xref:System.Windows.Media.GeometryDrawing> 使您通过将 <xref:System.Windows.Media.Pen> 和 <xref:System.Windows.Media.Brush> 与 <xref:System.Windows.Media.Geometry> 相关联来创建具有填充和轮廓的形状。  <xref:System.Windows.Media.GeometryDrawing.Geometry%2A> 描述形状的结构，<xref:System.Windows.Media.GeometryDrawing.Brush%2A> 描述形状的填充，<xref:System.Windows.Media.GeometryDrawing.Pen%2A> 描述形状的轮廓。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.GeometryDrawing> 来呈现形状。  该形状由 <xref:System.Windows.Media.GeometryGroup> 和两个 <xref:System.Windows.Media.EllipseGeometry> 对象进行描述。  形状内部使用 <xref:System.Windows.Media.LinearGradientBrush> 进行绘制，其轮廓则使用 <xref:System.Windows.Media.Brushes.Black%2A> <xref:System.Windows.Media.Pen> 进行绘制。  使用 <xref:System.Windows.Media.ImageDrawing> 和 <xref:System.Windows.Controls.Image> 元素显示 <xref:System.Windows.Media.GeometryDrawing>。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GeometryDrawingExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GeometryDrawingExample.cs#geometrydrawingexamplewholepage)]
 [!code-xml[DrawingMiscSnippets_snip#GeometryDrawingExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GeometryDrawingExample.xaml#geometrydrawingexamplewholepage)]  
  
 下面的插图显示生成的 <xref:System.Windows.Media.GeometryDrawing>。  
  
 ![两个椭圆的 GeometryDrawing](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-geodraw.png "graphicsmm\_geodraw")  
  
 若要创建更复杂的绘图，您可以使用 <xref:System.Windows.Media.DrawingGroup> 将多个绘图对象合并为一个合成绘图。  
  
## 请参阅  
 <xref:System.Windows.Media.DrawingGroup>   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [创建复合绘图](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-composite-drawing.md)