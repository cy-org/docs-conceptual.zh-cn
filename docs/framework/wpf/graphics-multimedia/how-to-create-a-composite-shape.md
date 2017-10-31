---
title: "如何：创建复合形状 | Microsoft Docs"
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
  - "复合形状"
  - "图形, 复合形状"
  - "形状, 复合"
ms.assetid: 8e5c7ef4-d7ed-4c43-afc9-ca01325c300b
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：创建复合形状
此示例演示如何使用 <xref:System.Windows.Media.Geometry> 对象创建复合形状并使用 <xref:System.Windows.Shapes.Path> 元素显示这些复合形状。  在下面的示例中，将 <xref:System.Windows.Media.LineGeometry>、<xref:System.Windows.Media.EllipseGeometry>、<xref:System.Windows.Media.RectangleGeometry> 与 <xref:System.Windows.Media.GeometryGroup> 一起使用以创建复合形状。  然后，使用 <xref:System.Windows.Shapes.Path> 元素绘制这些几何图形。  
  
## 示例  
 [!code-xml[GeometrySample#19](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#19)]  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#CompositeShapeCodeExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/CompositeShapeExample.cs#compositeshapecodeexampleinline1)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#CompositeShapeCodeExampleInline1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/compositeshapeexample.vb#compositeshapecodeexampleinline1)]  
  
 下图显示在上一示例中创建的形状。  
  
 ![使用 GeometryGroup 创建的复合几何图形](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-compositegeometryexample1.png "wcpsdk\_graphicsmm\_compositegeometryexample1")  
复合几何图形  
  
 更复杂的形状（如多边形和含曲线线段的形状）可使用 <xref:System.Windows.Media.PathGeometry> 创建。  有关演示如何使用 <xref:System.Windows.Media.PathGeometry> 创建形状的示例，请参见[使用 PathGeometry 创建形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md)。  尽管此示例使用 <xref:System.Windows.Shapes.Path> 元素向屏幕呈现形状，但 <xref:System.Windows.Media.Geometry> 对象也可用来描述 <xref:System.Windows.Media.GeometryDrawing> 或 <xref:System.Windows.Media.DrawingContext> 的内容。  此外，这些对象还可用于剪裁和命中测试。  
  
 此示例摘自一个更大的示例；有关完整示例，请参见 [Geometries Sample](http://go.microsoft.com/fwlink/?LinkID=159989)（几何图形示例）。