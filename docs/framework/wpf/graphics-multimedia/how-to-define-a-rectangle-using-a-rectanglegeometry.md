---
title: "如何：使用 RectangleGeometry 定义矩形 | Microsoft Docs"
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
  - "类, RectangleGeometry"
  - "图形 [WPF], 矩形"
  - "RectangleGeometry 类"
  - "矩形, 使用 RectangleGeometry 类创建"
ms.assetid: e40b8a8e-54b8-416b-a9f2-be6dca9fdf0b
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用 RectangleGeometry 定义矩形
本示例介绍如何使用 <xref:System.Windows.Media.RectangleGeometry> 类来描绘矩形。  
  
## 示例  
 下面的示例演示如何创建和呈现 <xref:System.Windows.Media.RectangleGeometry>。  矩形的相对位置和尺寸由 <xref:System.Windows.Rect> 结构定义。  相对位置是 `50,50`，高度和宽度均为 `25`，这将创建一个正方形。  矩形的内部是使用 <xref:System.Windows.Media.Brushes.LemonChiffon%2A> 画笔绘制的，它的轮廓是用厚度为 `1` 的 <xref:System.Windows.Media.Brushes.Black%2A> 笔画绘制的。  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMRectangleGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmrectanglegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmrectanglegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmrectanglegeometryexample)]  
  
 ![一个 RectangleGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rectangle.png "graphicsmm\_rectangle")  
RectangleGeometry  
  
 尽管此示例使用 <xref:System.Windows.Shapes.Path> 元素来呈现 <xref:System.Windows.Media.RectangleGeometry>，但还可以通过许多其他方法来使用 <xref:System.Windows.Media.RectangleGeometry> 对象。  例如，<xref:System.Windows.Media.RectangleGeometry> 可用于指定 <xref:System.Windows.UIElement> 的 <xref:System.Windows.UIElement.Clip%2A>，或者指定 <xref:System.Windows.Media.GeometryDrawing> 的 <xref:System.Windows.Media.GeometryDrawing.Geometry%2A>。  
  
 其他简单的几何图形类包括 <xref:System.Windows.Media.LineGeometry> 和 <xref:System.Windows.Media.EllipseGeometry>。  使用 <xref:System.Windows.Media.PathGeometry> 或 <xref:System.Windows.Media.StreamGeometry> 也可以创建这些几何图形和更复杂的几何图形。  
  
## 请参阅  
 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [创建复合形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-composite-shape.md)   
 [使用 PathGeometry 创建形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md)