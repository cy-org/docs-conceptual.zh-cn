---
title: "如何：在 PathGeometry 内部创建多个子路径 | Microsoft Docs"
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
  - "图形 [WPF], 子路径"
  - "多个子路径"
  - "PathGeometry 类"
  - "子路径"
ms.assetid: 104a862c-dde2-4e62-ac87-80660dd1681c
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在 PathGeometry 内部创建多个子路径
下面的示例演示如何在 <xref:System.Windows.Media.PathGeometry> 中创建多个子路径。  若要创建多个子路径，可以为每个子路径创建一个 <xref:System.Windows.Media.PathFigure>。  
  
## 示例  
 下面的示例创建了两个子路径，每个子路径都绘制一个三角形。  
  
 [!code-xml[GeometrySample#38](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#38)]  
  
 下面的示例演示如何使用 <xref:System.Windows.Shapes.Path> 和 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 特性语法来创建多个子路径。  每个 `M` 都创建一个新的子路径，以便该示例创建两个分别会创建一个三角形的子路径。  
  
 [!code-xml[GeometrySample#58](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/geometryattributesyntaxexample.xaml#58)]  
  
 （请注意，此特性语法实际上会创建一个 <xref:System.Windows.Media.StreamGeometry>（<xref:System.Windows.Media.PathGeometry> 的轻量版本）。  有关更多信息，请参见[路径标记语法](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)页。）  
  
## 请参阅  
 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)