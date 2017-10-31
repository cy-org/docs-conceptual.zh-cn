---
title: "如何：圆化 RectangleGeometry 的角 | Microsoft Docs"
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
  - "角, 倒圆"
  - "图形, 对 RectangleGeometry 对象进行倒圆角"
  - "RectangleGeometry 类, 倒圆角"
  - "对 RectangleGeometry 对象进行倒圆角"
ms.assetid: 926644bc-1357-4c0b-ac81-694bd090ae87
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：圆化 RectangleGeometry 的角
若要圆化 <xref:System.Windows.Media.RectangleGeometry> 的角，请将其 <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> 和 <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> 属性设置为大于零的值。  值越大，矩形的角越圆。  
  
## 示例  
 下面的示例演示具有不同的 <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> 和 <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> 设置的多个 <xref:System.Windows.Media.RectangleGeometry> 对象。  <xref:System.Windows.Media.RectangleGeometry> 对象使用 <xref:System.Windows.Shapes.Path> 元素来显示。  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMRoundedRectangleGeometryExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/RectangleGeometryRoundedCornerExample.xaml#graphicsmmroundedrectanglegeometryexamplewholepage)]  
  
 ![具有不同的 RadiusX&#47;RadiusY 设置的矩形](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rounded.png "graphicsmm\_rounded")  
带圆角的矩形  
  
## 请参阅  
 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [创建复合形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-composite-shape.md)   
 [使用 PathGeometry 创建形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md)