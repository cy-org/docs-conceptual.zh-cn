---
title: "GDI+ 中的开放曲线和闭合曲线 | Microsoft Docs"
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
  - "曲线"
  - "曲线, 绘图"
  - "曲线, 填充"
  - "GDI+, 曲线"
ms.assetid: 08d2cc9a-dc9d-4eed-bcbb-2c8e2ca5d3ae
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# GDI+ 中的开放曲线和闭合曲线
下面的插图显示了两条曲线：一条打开的和一条闭合的。  
  
 ![开放曲线和闭合曲线](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art24.png "Aboutgdip02\_art24")  
  
## 曲线的管理界面  
 闭合的曲线具有内部，因此可以用画笔填充。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 中的 <xref:System.Drawing.Graphics> 类提供了以下几种填充闭合形状和曲线的方法：<xref:System.Drawing.Graphics.FillRectangle%2A>、 <xref:System.Drawing.Graphics.FillEllipse%2A>、<xref:System.Drawing.Graphics.FillPie%2A>、<xref:System.Drawing.Graphics.FillPolygon%2A>、 <xref:System.Drawing.Graphics.FillClosedCurve%2A>、<xref:System.Drawing.Graphics.FillPath%2A> 和 <xref:System.Drawing.Graphics.FillRegion%2A>。  只要调用其中有一个方法，就必须将一个特定的画笔类型（<xref:System.Drawing.SolidBrush>、<xref:System.Drawing.Drawing2D.HatchBrush>、<xref:System.Drawing.TextureBrush>、<xref:System.Drawing.Drawing2D.LinearGradientBrush> 或 <xref:System.Drawing.Drawing2D.PathGradientBrush>）作为参数传递。  
  
 <xref:System.Drawing.Graphics.FillPie%2A> 方法与 <xref:System.Drawing.Graphics.DrawArc%2A> 方法类似。  正如 <xref:System.Drawing.Graphics.DrawArc%2A> 方法绘制椭圆的一部分轮廓一样，<xref:System.Drawing.Graphics.FillPie%2A> 方法填充椭圆内部的一部分。  下面的示例绘制了一个弧形并填充椭圆内部的相应部分：  
  
 [!code-csharp[LinesCurvesAndShapes#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#21)]
 [!code-vb[LinesCurvesAndShapes#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#21)]  
  
 下面的插图显示了该弧形和填充后的扇形。  
  
 ![开放曲线和闭合曲线](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art25.png "Aboutgdip02\_art25")  
  
 <xref:System.Drawing.Graphics.FillClosedCurve%2A> 方法与 <xref:System.Drawing.Graphics.DrawClosedCurve%2A> 方法类似。  这两种方法都通过连接结束点和起始点来自动闭合曲线。  下面的示例绘制了一条经过 \(0, 0\)、\(60, 20\) 和 \(40, 50\) 的曲线。  然后，该曲线通过连接 \(40, 50\) 至起始点 \(0, 0\) 自动闭合，并且用一种纯色填充内部。  
  
 [!code-csharp[LinesCurvesAndShapes#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#22)]
 [!code-vb[LinesCurvesAndShapes#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#22)]  
  
 <xref:System.Drawing.Graphics.FillPath%2A> 方法填充了路径的不同部分的内部。  如果路径的某一部分不构成封闭的曲线或图形，<xref:System.Drawing.Graphics.FillPath%2A> 方法会在填充该部分之前先自动将其闭合。  下面的示例绘制并填充一个路径，该路径由弧形、基数样条、字符串和扇形组成：  
  
 [!code-csharp[LinesCurvesAndShapes#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#23)]
 [!code-vb[LinesCurvesAndShapes#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#23)]  
  
 下面的插图显示了有纯色填充和没有纯色填充的路径。  请注意，用 <xref:System.Drawing.Graphics.DrawPath%2A> 方法得到的字符串中的文本是空心的，而不是实心的。  <xref:System.Drawing.Graphics.FillPath%2A> 方法可用于绘制字符串中字符的内部。  
  
 ![路径中的字符串](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art26.png "Aboutgdip02\_art26")  
  
## 请参阅  
 <xref:System.Drawing.Drawing2D.GraphicsPath?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 <xref:System.Drawing.Point?displayProperty=fullName>   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [如何：创建用于绘制的 Graphics 对象](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [构造并绘制轨迹](../../../../docs/framework/winforms/advanced/constructing-and-drawing-paths.md)