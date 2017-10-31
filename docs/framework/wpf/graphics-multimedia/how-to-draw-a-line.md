---
title: "如何：绘制线条 | Microsoft Docs"
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
  - "绘图, 文本行"
  - "图形 [WPF], 文本行"
  - "文本行, 绘图"
ms.assetid: 0513ee01-6b27-4bb3-85f3-3a3e6710d80e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：绘制线条
下面的示例演示如何使用 <xref:System.Windows.Shapes.Line> 元素来绘制线条。  
  
 若要绘制线条，请创建一个 <xref:System.Windows.Shapes.Line> 元素。  使用该元素的 <xref:System.Windows.Shapes.Line.X1%2A> 和 <xref:System.Windows.Shapes.Line.Y1%2A> 属性设置线条起点，并使用该元素的 <xref:System.Windows.Shapes.Line.X2%2A> 和 <xref:System.Windows.Shapes.Line.Y2%2A> 属性来设置线条终点。  最后，设置该元素的 <xref:System.Windows.Shapes.Shape.Stroke%2A> 和 <xref:System.Windows.Shapes.Shape.StrokeThickness%2A>，因为没有笔画的线条是看不见的。  
  
 为线条设置 <xref:System.Windows.Shapes.Shape.Fill%2A> 元素将毫无意义，因为线条没有内部区域。  
  
 下面的示例将在 <xref:System.Windows.Controls.Canvas> 元素内部绘制三个线条。  
  
## 示例  
 [!code-xml[drawingwithshapeelements#LineExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/lineexample.xaml#lineexample1)]  
  
 此示例摘自一个更大的示例；有关完整示例，请参见 [Shape Elements Sample](http://go.microsoft.com/fwlink/?LinkID=160037)（Shape 元素示例）。  
  
## 请参阅  
 <xref:System.Windows.Shapes.Line>   
 [Shape Elements Sample](http://go.microsoft.com/fwlink/?LinkID=160037)