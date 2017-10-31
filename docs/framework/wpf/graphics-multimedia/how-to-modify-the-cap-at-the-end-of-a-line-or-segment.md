---
title: "如何：修改线条或线段末端的线帽 | Microsoft Docs"
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
  - "图形, 形状线帽"
  - "Shape 元素, 线帽"
  - "Shape 元素, 结尾"
ms.assetid: f4bf3416-b3d8-4568-b98e-3eda8f6dbf7a
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：修改线条或线段末端的线帽
此示例演示如何在开放式 <xref:System.Windows.Shapes.Shape> 元素的起点和终点修改形状。  若要在开放式 <xref:System.Windows.Shapes.Shape> 的起点更改线帽，请使用其 <xref:System.Windows.Shapes.Shape.StrokeStartLineCap%2A> 属性。  若要在开放式 <xref:System.Windows.Shapes.Shape> 的终点更改线帽，请使用其 <xref:System.Windows.Shapes.Shape.StrokeEndLineCap%2A> 属性。  若要查看可用的线帽，请参见 <xref:System.Windows.Media.PenLineCap> 枚举。  
  
> [!NOTE]
>  此属性只影响开放式形状，如 <xref:System.Windows.Shapes.Line>、<xref:System.Windows.Shapes.Polyline> 或开放式 <xref:System.Windows.Shapes.Path> 元素。  
  
 下面的示例绘制了四个 <xref:System.Windows.Shapes.Polyline> 元素并在每个元素的终点处使用不同的一组形状。  
  
## 示例  
 [!code-xml[drawingwithshapeelements#ShapeLineCaps1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/linecapsandjoinsexample.xaml#shapelinecaps1)]  
  
 此示例摘自一个更大的示例；有关完整示例，请参见 [Shape Elements Sample](http://go.microsoft.com/fwlink/?LinkID=160037)（Shape 元素示例）。  
  
## 请参阅  
 <xref:System.Windows.Shapes.Polyline>   
 <xref:System.Windows.Media.PenLineCap>