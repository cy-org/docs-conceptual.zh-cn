---
title: "GDI+ 中的图形路径 | Microsoft Docs"
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
  - "绘图, 路径"
  - "GDI+, 绘制路径"
  - "图形, 路径"
  - "路径, 绘图"
ms.assetid: a5500dec-666c-41fd-9da3-2169dd89c5eb
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# GDI+ 中的图形路径
路径是通过组合直线、矩形和简单的曲线而形成的。  请回忆一下 [向量图形概述](../../../../docs/framework/winforms/advanced/vector-graphics-overview.md) 中的内容，以下基本构造块已被证明对于绘制图形是非常有用的：  
  
-   行  
  
-   矩形  
  
-   椭圆  
  
-   弧线  
  
-   多边形  
  
-   基数样条  
  
-   贝塞尔样条  
  
 在 GDI\+ 中，<xref:System.Drawing.Drawing2D.GraphicsPath> 对象您允许将这些构造块序列收集到一个单元中。  调用一次 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawPath%2A> 方法，就可以绘制出整个序列的直线、矩形、多边形和曲线。  下面的插图显示了通过组合一条直线、一段弧、一个贝塞尔样条和一个基数样条而创建的路径。  
  
 ![路径](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art14.png "Aboutgdip02\_art14")  
  
## 使用路径  
 <xref:System.Drawing.Drawing2D.GraphicsPath> 类提供了下列方法来创建要绘制的项序列：<xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A>、<xref:System.Drawing.Drawing2D.GraphicsPath.AddRectangle%2A>、<xref:System.Drawing.Drawing2D.GraphicsPath.AddEllipse%2A>、<xref:System.Drawing.Drawing2D.GraphicsPath.AddArc%2A>、<xref:System.Drawing.Drawing2D.GraphicsPath.AddPolygon%2A>、<xref:System.Drawing.Drawing2D.GraphicsPath.AddCurve%2A>（针对基数样条）和 <xref:System.Drawing.Drawing2D.GraphicsPath.AddBezier%2A>。  这些方法中的每一种都是重载的，即每种方法都支持几个不同的参数列表。  例如，<xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A> 方法的一个变体接收四个整数，<xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A> 方法的另一个变体则接收两个 <xref:System.Drawing.Point> 对象。  
  
 将直线、矩形和贝塞尔样条添加到路径的方法具有多个伴随方法，这些伴随方法在一次调用中将多个项添加到路径：<xref:System.Drawing.Drawing2D.GraphicsPath.AddLines%2A>、<xref:System.Drawing.Drawing2D.GraphicsPath.AddRectangles%2A> 和 <xref:System.Drawing.Drawing2D.GraphicsPath.AddBeziers%2A>。  同样，<xref:System.Drawing.Drawing2D.GraphicsPath.AddCurve%2A> 和 <xref:System.Drawing.Drawing2D.GraphicsPath.AddArc%2A> 方法也有几个将闭合的曲线或扇形添加到路径的伴随方法：<xref:System.Drawing.Drawing2D.GraphicsPath.AddClosedCurve%2A> 和 <xref:System.Drawing.Drawing2D.GraphicsPath.AddPie%2A>。  
  
 若要绘制路径，需要 <xref:System.Drawing.Graphics> 对象、<xref:System.Drawing.Pen> 对象和 <xref:System.Drawing.Drawing2D.GraphicsPath> 对象。  <xref:System.Drawing.Graphics> 对象提供 <xref:System.Drawing.Graphics.DrawPath%2A> 方法，<xref:System.Drawing.Pen> 对象存储用于呈现路径的线条特性，如宽度和颜色。  <xref:System.Drawing.Drawing2D.GraphicsPath> 对象存储构成路径的直线和曲线序列。  <xref:System.Drawing.Pen> 对象和 <xref:System.Drawing.Drawing2D.GraphicsPath> 对象作为参数传递给 <xref:System.Drawing.Graphics.DrawPath%2A> 方法。  下面的示例绘制了由直线、椭圆和贝塞尔样条组成的路径：  
  
 [!code-csharp[LinesCurvesAndShapes#101](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#101)]
 [!code-vb[LinesCurvesAndShapes#101](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#101)]  
  
 下面的插图显示了该路径。  
  
 ![路径](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art15.png "Aboutgdip02\_art15")  
  
 除了向路径添加直线、矩形和曲线外，还可以向路径添加路径。  这就允许您合并现有的路径来形成大型复杂路径。  
  
 [!code-csharp[LinesCurvesAndShapes#102](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#102)]
 [!code-vb[LinesCurvesAndShapes#102](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#102)]  
  
 您还可以把其他两个项目加入路径：字符串和扇形。  扇形是椭圆内的一部分。  下面的示例用弧形、基数样条、字符串和扇形创建了路径：  
  
 [!code-csharp[LinesCurvesAndShapes#103](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#103)]
 [!code-vb[LinesCurvesAndShapes#103](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#103)]  
  
 下面的插图显示了该路径。  请注意，不必连接路径；弧形、基数样条、字符串和扇形都是分开的。  
  
 ![路径](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art16.png "Aboutgdip02\_Art16")  
  
## 请参阅  
 <xref:System.Drawing.Drawing2D.GraphicsPath?displayProperty=fullName>   
 <xref:System.Drawing.Point?displayProperty=fullName>   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [如何：创建用于绘制的 Graphics 对象](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [构造并绘制轨迹](../../../../docs/framework/winforms/advanced/constructing-and-drawing-paths.md)