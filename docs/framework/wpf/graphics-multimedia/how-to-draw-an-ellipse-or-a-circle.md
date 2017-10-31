---
title: "如何：绘制椭圆或圆 | Microsoft Docs"
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
  - "圆形, 绘图"
  - "绘制圆形"
  - "绘制椭圆"
  - "椭圆, 绘图"
  - "图形, 绘制圆形"
  - "图形, 绘制椭圆"
ms.assetid: 99763b8c-bfc8-44be-8231-8a70daf5481a
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：绘制椭圆或圆
此示例演示如何通过使用 <xref:System.Windows.Shapes.Ellipse> 元素绘制椭圆或圆。  若要绘制椭圆，请创建一个 <xref:System.Windows.Shapes.Ellipse> 元素并指定其 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A>。  使用其 <xref:System.Windows.Shapes.Shape.Fill%2A> 属性来指定用于绘制椭圆内部区域的 <xref:System.Windows.Media.Brush>。  使用其 <xref:System.Windows.Shapes.Shape.Stroke%2A> 属性来指定用于绘制椭圆轮廓的 <xref:System.Windows.Media.Brush>。  <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> 属性指定椭圆轮廓的粗细。  
  
 若要绘制圆，请将 <xref:System.Windows.Shapes.Ellipse> 元素的 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 设置为彼此相等。  
  
 下面的示例将在 <xref:System.Windows.Controls.Canvas> 内绘制四个 <xref:System.Windows.Shapes.Ellipse> 元素。  
  
## 示例  
 [!code-xml[drawingwithshapeelements#EllipseExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/ellipseexample.xaml#ellipseexample1)]  
  
 虽然此示例使用 <xref:System.Windows.Controls.Canvas> 来包含椭圆，但是您可以使用椭圆元素（和所有其他形状元素）以及任何支持非文本内容的 <xref:System.Windows.Controls.Panel> 或 <xref:System.Windows.Controls.Control>。  
  
 此示例摘自一个更大的示例；有关完整示例，请参见 [Shape Elements Sample](http://go.microsoft.com/fwlink/?LinkID=160037)（Shape 元素示例）。  
  
## 请参阅  
 <xref:System.Windows.Shapes.Ellipse>   
 <xref:System.Windows.Shapes.Shape>   
 [Shape Elements Sample](http://go.microsoft.com/fwlink/?LinkID=160037)