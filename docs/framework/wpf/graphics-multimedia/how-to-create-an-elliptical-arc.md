---
title: "如何：创建椭圆弧 | Microsoft Docs"
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
  - "弧形, 椭圆"
  - "椭圆弧形, 创建"
  - "图形 [WPF], 椭圆弧形"
ms.assetid: 3dcfe502-3485-45de-99fb-d53a1367c484
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：创建椭圆弧
此示例演示如何绘制椭圆弧。  若要创建椭圆弧，请使用 <xref:System.Windows.Media.PathGeometry>、<xref:System.Windows.Media.PathFigure> 和 <xref:System.Windows.Media.ArcSegment> 类。  
  
## 示例  
 在下面的示例中，椭圆弧是从 \(10,100\) 到 \(200,100\) 绘制而成的。  该弧的 <xref:System.Windows.Media.ArcSegment.Size%2A> 为 100 x 50 个与设备无关的像素、<xref:System.Windows.Media.ArcSegment.RotationAngle%2A> 为 45 度、<xref:System.Windows.Media.ArcSegment.IsLargeArc%2A> 设置为 `true`、<xref:System.Windows.Media.ArcSegment.SweepDirection%2A> 为 <xref:System.Windows.Media.SweepDirection>。  
  
 \[xaml\]  
  
 在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中，可以使用特性语法来描述路径。  
  
 [!code-xml[GeometrySample#56](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/geometryattributesyntaxexample.xaml#56)]  
  
 \[xaml\]  
  
 （请注意，此特性语法实际上会创建一个 <xref:System.Windows.Media.StreamGeometry>（<xref:System.Windows.Media.PathGeometry> 的轻量版本）。  有关更多信息，请参见[路径标记语法](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)页。）  
  
 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，还可以通过显式使用对象标记来绘制椭圆弧。  下面的内容等效于前面的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记。  
  
 [!code-xml[GeometrySample#36](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#36)]  
  
 此示例摘自一个更大的示例。  有关完整示例，请参见 [Geometries Sample](http://go.microsoft.com/fwlink/?LinkID=159989)（几何示例）。  
  
## 请参阅  
 [创建二次贝塞尔曲线](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-quadratic-bezier-curve.md)   
 [创建三次方贝塞尔曲线](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-cubic-bezier-curve.md)