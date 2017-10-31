---
title: "如何：绘制矩形 | Microsoft Docs"
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
  - "绘图, 矩形"
  - "图形 [WPF], 矩形"
  - "矩形, 绘图"
ms.assetid: beeb57ef-fab5-4446-a38a-1588f97b4c2f
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：绘制矩形
下面的示例演示如何使用 <xref:System.Windows.Shapes.Rectangle> 元素来绘制矩形。  
  
 若要绘制矩形，请创建一个 <xref:System.Windows.Shapes.Rectangle> 元素并指定其 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A>。  若要在矩形内部进行绘制，请设置其 <xref:System.Windows.Shapes.Shape.Fill%2A>。  若要绘制矩形轮廓，请使用其 <xref:System.Windows.Shapes.Shape.Stroke%2A> 和 <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> 属性。  
  
 若要绘制矩形圆角，请指定可选的 <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> 和 <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> 属性。  <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> 和 <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> 属性设置用于使矩形的角变圆的椭圆的 x 轴和 y 轴半径。  
  
 以下示例在 <xref:System.Windows.Controls.Canvas> 中绘制了两个 <xref:System.Windows.Shapes.Rectangle> 元素。  第一个矩形内部为 <xref:System.Windows.Media.Brushes.Blue%2A>。  第二个矩形内部为 <xref:System.Windows.Media.Brushes.Blue%2A>、并且具有 <xref:System.Windows.Media.Brushes.Black%2A> 轮廓和圆角。  
  
## 示例  
 [!code-xml[drawingwithshapeelements#Rectangle1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/rectangleexample.xaml#rectangle1)]  
  
 虽然此示例使用 <xref:System.Windows.Controls.Canvas> 来包含矩形，但是您可以使用矩形元素（和所有其他形状元素）以及任何支持非文本内容的 <xref:System.Windows.Controls.Panel> 或 <xref:System.Windows.Controls.Control>。  事实上，在为 <xref:System.Windows.Controls.Grid> 面板的某些部分提供背景时矩形特别有用。  有关示例，请参见 [表概述](../../../../docs/framework/wpf/advanced/table-overview.md)。  
  
 此示例摘自一个更大的示例；有关完整示例，请参见 [Shape Elements Sample](http://go.microsoft.com/fwlink/?LinkID=160037)（Shape 元素示例）。  
  
## 请参阅  
 <xref:System.Windows.Shapes.Rectangle>   
 [Shape Elements Sample](http://go.microsoft.com/fwlink/?LinkID=160037)   
 [WPF 中的形状和基本绘图概述](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)   
 [表概述](../../../../docs/framework/wpf/advanced/table-overview.md)