---
title: "如何：使用多边形元素来绘制闭合形状 | Microsoft Docs"
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
  - "闭合形状, 使用多边形元素进行绘制"
  - "绘图, 使用多边形元素绘制闭合形状"
  - "图形, 多边形元素"
  - "多边形元素"
ms.assetid: 4b0ca008-29ce-48dd-8bc3-f3a20ffca6a6
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使用多边形元素来绘制闭合形状
此示例演示如何使用 <xref:System.Windows.Shapes.Polygon> 元素绘制闭合形状。  若要绘制闭合形状，请创建一个 <xref:System.Windows.Shapes.Polygon> 元素，并使用其 <xref:System.Windows.Shapes.Polygon.Points%2A> 属性指定形状的顶点。  系统将自动绘制一条线连接第一个点和最后一个点。  最后，指定 <xref:System.Windows.Shapes.Shape.Fill%2A> 和\/或 <xref:System.Windows.Shapes.Shape.Stroke%2A>。  
  
## 示例  
 在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中，点的有效语法是由逗号分隔的 x 和 y 坐标对组成的空格分隔列表。  
  
 [!code-xml[drawingwithshapeelements#PolygonExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/polygonexample.xaml#polygonexample1)]  
  
 虽然此示例使用 <xref:System.Windows.Controls.Canvas> 来包含多边形，但您可以将多边形元素（及所有其他形状元素）与支持非文本内容的任何 <xref:System.Windows.Controls.Panel> 或 <xref:System.Windows.Controls.Control> 一起使用。  
  
 此示例摘自一个更大的示例；有关完整示例，请参见 [Shape Elements Sample](http://go.microsoft.com/fwlink/?LinkID=160037)（Shape 元素示例）。