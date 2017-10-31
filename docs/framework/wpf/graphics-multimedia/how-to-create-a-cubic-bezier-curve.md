---
title: "如何：创建三次方贝塞尔曲线 | Microsoft Docs"
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
  - "贝塞尔曲线, 三次方"
  - "创建, 三次方贝塞尔曲线"
  - "三次方贝塞尔曲线"
  - "曲线, 三次方贝塞尔曲线"
  - "图形, 三次方贝塞尔曲线"
ms.assetid: 450a3a77-7c57-48b0-a008-0f6051add980
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：创建三次方贝塞尔曲线
此示例演示如何创建三次方贝塞尔曲线。  若要创建三次方贝塞尔曲线，请使用 <xref:System.Windows.Media.PathGeometry>、<xref:System.Windows.Media.PathFigure> 和 <xref:System.Windows.Media.BezierSegment> 类。  若要显示所生成的几何图形，请使用 <xref:System.Windows.Shapes.Path> 元素，或将该元素与 <xref:System.Windows.Media.GeometryDrawing> 或 <xref:System.Windows.Media.DrawingContext> 一起使用。  在下面的示例中，三次方贝塞尔曲线从 \(10,100\) 绘制到 \(300,100\)。  该曲线具有 \(100,0\) 和 \(200,200\) 两个控制点。  
  
## 示例  
 \[xaml\]  
  
 在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中，可以使用缩写标记语法来描述路径。  
  
 [!code-xml[GeometrySample#53](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/geometryattributesyntaxexample.xaml#53)]  
  
 \[xaml\]  
  
 在[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，还可以使用对象标记来绘制三次方贝塞尔曲线。  下面的示例与前面的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 示例是等效的。  
  
 [!code-xml[GeometrySample#33](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#33)]  
  
 此示例摘自一个更大的示例；有关完整示例，请参见 [Geometries Sample](http://go.microsoft.com/fwlink/?LinkID=159989)（几何图形示例）。  
  
## 请参阅  
 [创建椭圆弧](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-an-elliptical-arc.md)   
 [在 PathGeometry 中创建 LineSegment](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-linesegment-in-a-pathgeometry.md)   
 [Create a Cubic Bezier Curve](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-cubic-bezier-curve.md)   
 [创建二次贝塞尔曲线](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-quadratic-bezier-curve.md)