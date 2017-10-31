---
title: "GDI+ 中的椭圆和弧线 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "弧形"
  - "绘图, 弧形"
  - "绘图, 椭圆"
  - "椭圆"
  - "GDI+, 弧形"
  - "GDI+, 椭圆"
ms.assetid: 34f35133-a835-4ca4-81f6-0dfedee8b683
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# GDI+ 中的椭圆和弧线
可以使用 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawEllipse%2A> 和 <xref:System.Drawing.Graphics.DrawArc%2A> 方法轻松绘制椭圆和弧线。  
  
## 绘制椭圆  
 若要绘制椭圆，需要有 <xref:System.Drawing.Graphics> 对象和 <xref:System.Drawing.Pen> 对象。  <xref:System.Drawing.Graphics> 对象提供 <xref:System.Drawing.Graphics.DrawEllipse%2A> 方法，<xref:System.Drawing.Pen> 对象存储用于呈现椭圆的线条特性，如宽度和颜色。  <xref:System.Drawing.Pen> 对象作为参数之一传递给 <xref:System.Drawing.Graphics.DrawEllipse%2A> 方法。  传递给 <xref:System.Drawing.Graphics.DrawEllipse%2A> 方法的其余参数指定椭圆的边框。  下面的插图显示了一个椭圆，以及它的边框。  
  
 ![椭圆和弧](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art05.png "Aboutgdip02\_art05")  
  
 下面的示例绘制了一个椭圆；边框的宽度为 80，高度为 40，左上角位于 \(100, 50\)：  
  
 [!code-csharp[LinesCurvesAndShapes#51](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#51)]
 [!code-vb[LinesCurvesAndShapes#51](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#51)]  
  
 <xref:System.Drawing.Graphics.DrawEllipse%2A> 是一种 <xref:System.Drawing.Graphics> 类的重载方法，因此您可以通过多种方式为它提供参数。  例如，您可以构造 <xref:System.Drawing.Rectangle> 并将 <xref:System.Drawing.Rectangle> 作为参数传递给 <xref:System.Drawing.Graphics.DrawEllipse%2A> 方法：  
  
 [!code-csharp[LinesCurvesAndShapes#52](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#52)]
 [!code-vb[LinesCurvesAndShapes#52](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#52)]  
  
## 绘制弧线  
 弧线是椭圆的一部分。  若要绘制弧线，可调用 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawArc%2A> 方法。  除了 <xref:System.Drawing.Graphics.DrawArc%2A> 需要有起始角度和仰角以外，<xref:System.Drawing.Graphics.DrawEllipse%2A> 方法的参数与 <xref:System.Drawing.Graphics.DrawArc%2A> 方法的参数相同。  下面的示例绘制了一个起始角为 30 度、仰角为 180 度的弧线：  
  
 [!code-csharp[LinesCurvesAndShapes#53](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#53)]
 [!code-vb[LinesCurvesAndShapes#53](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#53)]  
  
 下面的插图显示了弧线、椭圆和边框。  
  
 ![椭圆和弧](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art06.png "Aboutgdip02\_art06")  
  
## 请参阅  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [如何：创建用于绘制的 Graphics 对象](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [如何：创建钢笔](../../../../docs/framework/winforms/advanced/how-to-create-a-pen.md)   
 [如何：绘制空心形状](../../../../docs/framework/winforms/advanced/how-to-draw-an-outlined-shape.md)