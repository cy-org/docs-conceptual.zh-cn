---
title: "GDI+ 中的多边形 | Microsoft Docs"
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
  - "绘图, 多边形"
  - "GDI+, 多边形"
  - "多边形"
ms.assetid: a72213d2-d69a-4c2b-a75c-be7b20390c13
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# GDI+ 中的多边形
多边形是有三条或更多直边的闭合图形。  例如，三角形是有三条边的多边形，矩形是有四条边的多边形，五边形是有五条边的多边形。  下面的插图显示了几个多边形。  
  
 ![多边形](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art07.png "Aboutgdip02\_art07")  
  
## 绘制多边形  
 若要绘制多边形，需要 <xref:System.Drawing.Graphics> 对象、<xref:System.Drawing.Pen> 对象和 <xref:System.Drawing.Point>（或 <xref:System.Drawing.PointF>）对象数组。  <xref:System.Drawing.Graphics> 对象提供 <xref:System.Drawing.Graphics.DrawPolygon%2A> 方法。  <xref:System.Drawing.Pen> 对象存储用于呈现多边形的线条特性，例如宽度和颜色，<xref:System.Drawing.Point> 对象数组存储将由直线连接的点。  <xref:System.Drawing.Pen> 对象和 <xref:System.Drawing.Point> 对象数组作为参数传递给 <xref:System.Drawing.Graphics.DrawPolygon%2A> 方法。  下面的示例绘制了一个三条边的多边形。  请注意， `myPointArray` 中只有三个点：\(0, 0\)、\(50, 30\) 和 \(30, 60\)。  <xref:System.Drawing.Graphics.DrawPolygon%2A> 方法通过绘制一条从 \(30, 60\) 回到起点 \(0, 0\) 的直线来自动闭合多边形。  
  
 [!code-csharp[LinesCurvesAndShapes#111](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#111)]
 [!code-vb[LinesCurvesAndShapes#111](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#111)]  
  
 下面的插图显示了该多边形。  
  
 ![多边形](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art08.png "Aboutgdip02\_art08")  
  
## 请参阅  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [如何：创建钢笔](../../../../docs/framework/winforms/advanced/how-to-create-a-pen.md)