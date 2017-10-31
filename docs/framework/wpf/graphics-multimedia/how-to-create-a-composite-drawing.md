---
title: "如何：创建复合绘图 | Microsoft Docs"
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
  - "类, DrawingGroup"
  - "复合绘图"
  - "DrawingGroup 类"
  - "绘图, 复合"
  - "图形, 复合绘图"
ms.assetid: 066eb0ab-5f0e-439d-85c6-dca60af269fc
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：创建复合绘图
本示例演示如何使用 <xref:System.Windows.Media.DrawingGroup>，通过将多个 <xref:System.Windows.Media.Drawing> 对象组合为一个复合图形来创建复杂图形。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.DrawingGroup>，基于 <xref:System.Windows.Media.GeometryDrawing> 和 <xref:System.Windows.Media.ImageDrawing> 对象创建一个复合图形。  下面的插图演示此示例生成的输出。  
  
 ![具有多个绘图的 DrawingGroup](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-simple.png "graphicsmm\_simple")  
使用 DrawingGroup 创建的复合图形  
  
 请注意显示图形边界的灰色边框。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmsimpledrawinggroupexample)]
 [!code-xml[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmsimpledrawinggroupexample)]  
  
 可以使用 <xref:System.Windows.Media.DrawingGroup> 向它所包含的图形应用 <xref:System.Windows.Media.DrawingGroup.Transform%2A>、<xref:System.Windows.Media.DrawingGroup.Opacity%2A> 设置、<xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>、<xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>、<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A> 或 <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>。  因为 <xref:System.Windows.Media.DrawingGroup> 也是一个 <xref:System.Windows.Media.Drawing>，所以它可以包含其他 <xref:System.Windows.Media.DrawingGroup> 对象。  
  
 下面的示例与前面的示例类似，但它使用其他 <xref:System.Windows.Media.DrawingGroup> 对象来向某些图形应用位图效果和不透明蒙板。  下面的插图演示此示例生成的输出。  
  
 ![具有多个绘图的 DrawingGroup](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-multiple.png "graphicsmm\_multiple")  
具有多个 DrawingGroup 对象的复合图形  
  
 请注意显示图形边界的灰色边框。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMMultipleDrawingGroupsExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmmultipledrawinggroupsexample)]
 [!code-xml[DrawingMiscSnippets_snip#GraphicsMMMultipleDrawingGroupsExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmmultipledrawinggroupsexample)]  
  
 有关 <xref:System.Windows.Media.Drawing> 对象的更多信息，请参见 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>   
 <xref:System.Windows.Media.DrawingGroup.Transform%2A>   
 <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>   
 <xref:System.Windows.Media.DrawingGroup.Opacity%2A>   
 <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>   
 <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)