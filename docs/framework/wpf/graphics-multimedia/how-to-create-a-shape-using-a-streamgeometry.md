---
title: "如何：使用 StreamGeometry 创建形状 | Microsoft Docs"
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
  - "类, StreamGeometry"
  - "图形 [WPF], 形状"
  - "形状, 使用 StreamGeometry 类创建"
  - "StreamGeometry 类"
ms.assetid: 08f7c8ce-074b-49cd-9aba-cc9592d4ee51
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用 StreamGeometry 创建形状
<xref:System.Windows.Media.StreamGeometry> 是 <xref:System.Windows.Media.PathGeometry> 的一个轻型替代品，可用于创建几何形状。  当您需要描绘复杂的几何图形，但不希望因为支持数据绑定、动画或修改而引入系统开销时，可使用 <xref:System.Windows.Media.StreamGeometry>。  例如，由于具有高效率，<xref:System.Windows.Media.StreamGeometry> 类是描绘装饰物的理想选择。  
  
## 示例  
 下面的示例使用特性语法用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 创建一个三角形 <xref:System.Windows.Media.StreamGeometry>。  
  
 [!code-xml[GeometriesMiscSnippets_snip#StreamGeometryTriangleExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/StreamGeometryExample.xaml#streamgeometrytriangleexamplewholepage)]  
  
 有关 <xref:System.Windows.Media.StreamGeometry> 特性语法的更多信息，请参见[路径标记语法](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)页。  
  
## 示例  
 下一个示例使用 <xref:System.Windows.Media.StreamGeometry> 通过代码定义一个三角形。  首先，该示例创建一个 <xref:System.Windows.Media.StreamGeometry>，然后获取一个 <xref:System.Windows.Media.StreamGeometryContext> 并使用它来描绘三角形。  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#StreamGeometryTriangleExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/StreamGeometryTriangleExample.cs#streamgeometrytriangleexamplewholepage)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#StreamGeometryTriangleExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/streamgeometrytriangleexample.vb#streamgeometrytriangleexamplewholepage)]  
  
## 示例  
 下一个示例创建这样一个方法，该方法使用 <xref:System.Windows.Media.StreamGeometry> 和 <xref:System.Windows.Media.StreamGeometryContext> 基于指定的参数来定义一个几何形状。  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#StreamGeometryExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/StreamGeometryExample.cs#streamgeometryexamplewholepage)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#StreamGeometryExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/streamgeometryexample.vb#streamgeometryexamplewholepage)]  
  
## 请参阅  
 <xref:System.Windows.Media.PathGeometry>   
 <xref:System.Windows.Media.StreamGeometry>   
 <xref:System.Windows.Media.StreamGeometryContext>   
 [使用 PathGeometry 创建形状](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md)   
 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)