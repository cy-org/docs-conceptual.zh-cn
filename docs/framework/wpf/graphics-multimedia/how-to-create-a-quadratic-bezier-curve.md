---
title: "如何：创建二次贝塞尔曲线 | Microsoft Docs"
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
  - "贝塞尔曲线, 创建"
  - "图形 [WPF], 二次贝塞尔曲线"
  - "二次贝塞尔曲线, 创建"
ms.assetid: cd8fca4a-504e-4fd8-92ea-2969065a6e02
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：创建二次贝塞尔曲线
此示例演示如何创建二次贝塞尔曲线。  若要创建二次贝塞尔曲线，应使用 <xref:System.Windows.Media.PathGeometry>、<xref:System.Windows.Media.PathFigure> 和 <xref:System.Windows.Media.QuadraticBezierSegment> 类。  
  
## 示例  
 在下面的示例中，二次方贝塞尔曲线从 \(10,100\) 绘制到 \(300,100\)。  曲线的控制点为 \(200,200\)。  
  
 \[xaml\]  
  
 在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中，可以使用特性语法来描述路径。  
  
 [!code-xml[GeometrySample#54](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/geometryattributesyntaxexample.xaml#54)]  
  
 \[xaml\]  
  
 （请注意，此特性语法实际上会创建一个 <xref:System.Windows.Media.StreamGeometry>（<xref:System.Windows.Media.PathGeometry> 的轻量版本）。  有关更多信息，请参见[路径标记语法](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)页。）  
  
 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，您还可以使用对象元素语法绘制一条二次贝塞尔曲线。  下面的示例与前面的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 示例是等效的。  
  
 [!code-xml[GeometrySample#34](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#34)]  
  
 此示例摘自一个更大的示例；有关完整示例，请参见 [Geometries Sample](http://go.microsoft.com/fwlink/?LinkID=159989)（几何图形示例）。  
  
## 请参阅  
 [创建椭圆弧](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-an-elliptical-arc.md)   
 [创建三次方贝塞尔曲线](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-cubic-bezier-curve.md)