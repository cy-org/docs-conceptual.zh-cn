---
title: "如何：使用 Polyline 元素来绘制折线 | Microsoft Docs"
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
  - "连接的线"
  - "绘图, 折线"
  - "图形 [WPF], 折线"
  - "文本行, 连接的（请参见折线）"
  - "折线, 绘图"
ms.assetid: 65db8935-d047-4295-87c4-b427ff3ad293
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用 Polyline 元素来绘制折线
本示例演示如何通过 <xref:System.Windows.Shapes.Polyline> 元素绘制折线（一系列连接的线）。  
  
 若要绘制折线，请创建 <xref:System.Windows.Shapes.Polyline> 元素并使用其 <xref:System.Windows.Shapes.Polyline.Points%2A> 属性指定形状的顶点。  最后，使用 <xref:System.Windows.Shapes.Shape.Stroke%2A> 和 <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> 属性描绘折线轮廓，因为没有笔画的线是不可见的。  
  
> [!NOTE]
>  因为 <xref:System.Windows.Shapes.Polyline> 元素不是闭合形状，所以 <xref:System.Windows.Shapes.Shape.Fill%2A> 属性不起任何作用，即便您故意闭合形状轮廓也是如此。  若要使用 <xref:System.Windows.Shapes.Shape.Fill%2A> 创建闭合形状，请使用 <xref:System.Windows.Shapes.Polygon> 元素。  
  
 以下示例在 <xref:System.Windows.Controls.Canvas> 内部绘制了两个 <xref:System.Windows.Shapes.Polyline> 元素。  
  
## 示例  
 在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中，点的有效语法是由逗号分隔的 x 和 y 坐标对组成的空格分隔列表。  
  
 [!code-xml[drawingwithshapeelements#PolylineExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/polylineexample.xaml#polylineexample1)]  
  
 虽然此示例使用 <xref:System.Windows.Controls.Canvas> 来包含折线，但是您可以使用折线元素（和所有其他形状元素）以及任何支持非文本内容的 <xref:System.Windows.Controls.Panel> 或 <xref:System.Windows.Controls.Control>。  
  
 此示例摘自一个更大的示例；有关完整示例，请参见 [Shape Elements Sample](http://go.microsoft.com/fwlink/?LinkID=160037)（Shape 元素示例）。  
  
## 请参阅  
 <xref:System.Windows.Shapes.Polyline>   
 <xref:System.Windows.Shapes.Polygon>   
 <xref:System.Windows.Shapes.Shape>   
 [Shape Elements Sample](http://go.microsoft.com/fwlink/?LinkID=160037)   
 [WPF 中的形状和基本绘图概述](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)