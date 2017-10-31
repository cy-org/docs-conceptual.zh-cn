---
title: "如何：使用 LineGeometry 创建线条 | Microsoft Docs"
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
  - "类, LineGeometry"
  - "图形 [WPF], 文本行"
  - "LineGeometry 类"
ms.assetid: 41231b22-1f74-4c26-a8e7-a55b29f8f6bd
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使用 LineGeometry 创建线条
此示例演示如何使用 <xref:System.Windows.Media.LineGeometry> 类描述线条。  <xref:System.Windows.Media.LineGeometry> 由其起点和终点定义。  
  
## 示例  
 下面的示例演示如何创建并呈现 <xref:System.Windows.Media.LineGeometry>。  <xref:System.Windows.Shapes.Path> 元素用于呈现线条。  由于线条不包含区域，因此未指定 <xref:System.Windows.Shapes.Path> 对象的 <xref:System.Windows.Shapes.Shape.Fill%2A>；而改用 <xref:System.Windows.Shapes.Shape.Stroke%2A> 和 <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> 属性。  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMLineGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmlinegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmlinegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmlinegeometryexample)]  
  
 ![一个 LineGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-line.png "graphicsmm\_line")  
从 \(10,20\) 绘制到 \(100,130\) 的 LineGeometry  
  
 其他简单的几何图形类包括 <xref:System.Windows.Media.LineGeometry> 和 <xref:System.Windows.Media.EllipseGeometry>。  使用 <xref:System.Windows.Media.PathGeometry> 或 <xref:System.Windows.Media.StreamGeometry> 也可以创建这些几何图形和更复杂的几何图形。  有关更多信息，请参见 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)。  
  
## 请参阅  
 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [创建复合形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-composite-shape.md)   
 [使用 PathGeometry 创建形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md)