---
title: "如何：使用 PathGeometry 创建形状 | Microsoft Docs"
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
  - "类, PathGeometry"
  - "图形 [WPF], 形状"
  - "PathGeometry 类"
  - "形状, 使用 PathGeometry 类创建"
ms.assetid: 49a4a8b7-e738-45be-8dac-b54a6d8f5b21
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用 PathGeometry 创建形状
此示例演示如何使用 <xref:System.Windows.Media.PathGeometry> 类创建形状。  <xref:System.Windows.Media.PathGeometry> 对象由一个或多个 <xref:System.Windows.Media.PathFigure> 对象组成；每个 <xref:System.Windows.Media.PathFigure> 代表一个不同的“图形”或形状。  每个 <xref:System.Windows.Media.PathFigure> 自身又由一个或多个 <xref:System.Windows.Media.PathSegment> 对象组成，每个对象均表示图形或形状的已连接部分。  线段类型包括 <xref:System.Windows.Media.LineSegment>、<xref:System.Windows.Media.ArcSegment> 和 <xref:System.Windows.Media.BezierSegment>。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.PathGeometry> 创建三角形。  <xref:System.Windows.Media.PathGeometry> 通过使用 <xref:System.Windows.Shapes.Path> 元素来显示。  
  
 [!code-xml[GeometrySample#49](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#49)]  
  
 下图显示在上一示例中创建的形状。  
  
 ![一个 PathGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-pathgeometry-triangle.png "wcpsdk\_graphicsmm\_pathgeometry\_triangle")  
使用 PathGeometry 创建的三角形  
  
 上一示例演示了如何创建一个相对较简单的三角形形状。  <xref:System.Windows.Media.PathGeometry> 还可用于创建一些更为复杂的形状，包括弧线和曲线。  有关示例，请参见 [创建椭圆弧](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-an-elliptical-arc.md)、[创建三次方贝塞尔曲线](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-cubic-bezier-curve.md) 和 [创建二次贝塞尔曲线](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-quadratic-bezier-curve.md)。  
  
 此示例摘自一个更大的示例；有关完整示例，请参见 [Geometries Sample](http://go.microsoft.com/fwlink/?LinkID=159989)（几何图形示例）。  
  
## 请参阅  
 <xref:System.Windows.Shapes.Path>   
 <xref:System.Windows.Media.GeometryDrawing>   
 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [Geometries Sample](http://go.microsoft.com/fwlink/?LinkID=159989)