---
title: "GDI+ 中的笔、直线和矩形 | Microsoft Docs"
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
  - "绘图, 文本行"
  - "绘图, 矩形"
  - "示例 [Windows 窗体], 绘制线条和形状"
  - "示例 [Windows 窗体], GDI+"
  - "示例 [Windows 窗体], 钢笔"
  - "GDI+, 文本行"
  - "GDI+, 钢笔"
  - "GDI+, 矩形"
  - "文本行"
  - "文本行, 虚线"
  - "矩形"
ms.assetid: 30b25aae-e3eb-4479-bdb8-187cf651fc84
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# GDI+ 中的笔、直线和矩形
若要用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 绘制直线，需要创建 <xref:System.Drawing.Graphics> 对象和 <xref:System.Drawing.Pen> 对象。  <xref:System.Drawing.Graphics> 对象提供进行实际绘制的方法，<xref:System.Drawing.Pen> 对象存储特性，如直线的颜色、宽度和线型。  
  
## 绘制直线  
 若要绘制直线，请调用 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.DrawLine%2A> 方法。  将 <xref:System.Drawing.Pen> 对象作为参数之一传递给 <xref:System.Drawing.Graphics.DrawLine%2A> 方法。  下面的示例绘制了一条从点 \(4, 2\) 到点 \(12, 6\) 的直线：  
  
 [!code-csharp[LinesCurvesAndShapes#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#41)]
 [!code-vb[LinesCurvesAndShapes#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#41)]  
  
 <xref:System.Drawing.Graphics.DrawLine%2A> 是 <xref:System.Drawing.Graphics> 类的一个重载方法，因此，有数种为其提供参数的方式。  例如，可构造两个 <xref:System.Drawing.Point> 对象并将 <xref:System.Drawing.Point> 对象作为参数传递给 <xref:System.Drawing.Graphics.DrawLine%2A> 方法：  
  
 [!code-csharp[LinesCurvesAndShapes#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#42)]
 [!code-vb[LinesCurvesAndShapes#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#42)]  
  
## 构造钢笔  
 可以在构造 <xref:System.Drawing.Pen> 对象时指定某些特性。  例如，有一种 `Pen` 构造函数允许您指定颜色和宽度。  下面的示例绘制了一条从 \(0, 0\) 到 \(60, 30\) 宽度为 2 的蓝线：  
  
 [!code-csharp[LinesCurvesAndShapes#43](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#43)]
 [!code-vb[LinesCurvesAndShapes#43](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#43)]  
  
## 虚线和线帽  
 <xref:System.Drawing.Pen> 对象也公开属性（如 <xref:System.Drawing.Pen.DashStyle%2A>），这些属性可用于指定直线的特性。  下面的示例绘制了一条从 \(100, 50\) 到 \(300, 80\) 的虚线：  
  
 [!code-csharp[LinesCurvesAndShapes#44](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#44)]
 [!code-vb[LinesCurvesAndShapes#44](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#44)]  
  
 可以使用 <xref:System.Drawing.Pen> 对象的属性为直线设置更多特性。  <xref:System.Drawing.Pen.StartCap%2A> 属性和 <xref:System.Drawing.Pen.EndCap%2A> 属性指定直线端点的外观；端点可以是平的、方形的、圆形的、三角形的或自定义的形状。  <xref:System.Drawing.Pen.LineJoin%2A> 属性用于指定连接的线相互间是斜接的（联接时形成锐角）、斜切的、圆形的还是截断的。  下面的插图显示了具有不同的线帽和联接类型的直线。  
  
 ![直线](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art04.png "Aboutgdip02\_art04")  
  
## 绘制矩形  
 用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 绘制矩形与绘制直线类似。  若要绘制矩形，需要 <xref:System.Drawing.Graphics> 对象和 <xref:System.Drawing.Pen> 对象。  <xref:System.Drawing.Graphics> 对象提供 <xref:System.Drawing.Graphics.DrawRectangle%2A> 方法，<xref:System.Drawing.Pen> 对象存储特性（例如线宽和颜色）。  将 <xref:System.Drawing.Pen> 对象作为参数之一传递给 <xref:System.Drawing.Graphics.DrawRectangle%2A> 方法。  下面的示例绘制了一个矩形，其左上角位于 \(100, 50\)，宽度为 80，高度为 40：  
  
 [!code-csharp[LinesCurvesAndShapes#45](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#45)]
 [!code-vb[LinesCurvesAndShapes#45](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#45)]  
  
 <xref:System.Drawing.Graphics.DrawRectangle%2A> 是 <xref:System.Drawing.Graphics> 类的一个重载方法，因此，有数种为其提供参数的方式。  例如，可构造 <xref:System.Drawing.Rectangle> 对象并将 <xref:System.Drawing.Rectangle> 对象作为参数传递给 <xref:System.Drawing.Graphics.DrawRectangle%2A> 方法：  
  
 [!code-csharp[LinesCurvesAndShapes#46](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#46)]
 [!code-vb[LinesCurvesAndShapes#46](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#46)]  
  
 <xref:System.Drawing.Rectangle> 对象具有用于处理和收集矩形相关信息的方法和属性。  例如，<xref:System.Drawing.Rectangle.Inflate%2A> 和 <xref:System.Drawing.Rectangle.Offset%2A> 方法可更改矩形的大小和位置。  <xref:System.Drawing.Rectangle.IntersectsWith%2A> 方法判断矩形是否与另一给定矩形相交，<xref:System.Drawing.Rectangle.Contains%2A> 方法判断一个给定点是否在该矩形内。  
  
## 请参阅  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 <xref:System.Drawing.Rectangle?displayProperty=fullName>   
 [如何：创建钢笔](../../../../docs/framework/winforms/advanced/how-to-create-a-pen.md)   
 [如何：在 Windows 窗体上绘制线条](../../../../docs/framework/winforms/advanced/how-to-draw-a-line-on-a-windows-form.md)   
 [如何：绘制空心形状](../../../../docs/framework/winforms/advanced/how-to-draw-an-outlined-shape.md)