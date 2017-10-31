---
title: "向量图形概述 | Microsoft Docs"
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
  - "坐标系统"
  - "图形, 向量图形"
  - "两端均含的终结点"
ms.assetid: 0195df81-66be-452d-bb53-5a582ebfdc09
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 向量图形概述
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 在坐标系中绘制直线、矩形和其他形状。  您可以从各种各样的坐标系统中选择，但默认坐标系统的原点是在左上角，并且 x 轴指向右边，y 轴指向下边。  默认坐标系统的度量单位是像素。  
  
## GDI\+ 的构造块  
 ![矢量图形](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art01.png "AboutGdip02\_Art01")  
  
 计算机监视器是在一个点的矩形数组上创建其显示，这些点被称为图片元素或像素。  各台监视器屏幕上显示的像素数量都是不同的，并且用户通常在一定程度上可以配置单独一台监视器上显示的像素数量。  
  
 ![矢量图形](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art02.png "AboutGdip02\_Art02")  
  
 在使用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 绘制直线、矩形或曲线时，需要提供有关要绘制的项目的某些关键信息。  例如，可以通过提供两个点来指定一条直线，还可以通过提供一个点、高度和宽度来指定一个矩形。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 与显示设备驱动程序软件协同工作，以确定必须启用哪些像素来显示直线、矩形或曲线。  下面的插图显示了已打开的用于显示从点 \(4, 2\) 到点 \(12, 8\) 的直线的像素。  
  
 ![矢量图形](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art03.png "AboutGdip02\_Art03")  
  
 在实践中，人们发现某些基本构造块对于创建二维图片尤其有用。  下表中列出了 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 支持的构造块：  
  
-   行  
  
-   矩形  
  
-   椭圆  
  
-   弧线  
  
-   多边形  
  
-   基数样条  
  
-   贝塞尔样条  
  
## 使用图形对象进行绘制的方法  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 中的 <xref:System.Drawing.Graphics> 类提供了绘制前面列表中的各项的方法：<xref:System.Drawing.Graphics.DrawLine%2A>、<xref:System.Drawing.Graphics.DrawRectangle%2A>、<xref:System.Drawing.Graphics.DrawEllipse%2A>、<xref:System.Drawing.Graphics.DrawPolygon%2A>、<xref:System.Drawing.Graphics.DrawArc%2A>、<xref:System.Drawing.Graphics.DrawCurve%2A>（针对基数样条）和 <xref:System.Drawing.Graphics.DrawBezier%2A>。  这些方法中的每一种都是重载的，即每种方法都支持几个不同的参数列表。  例如，<xref:System.Drawing.Graphics.DrawLine%2A> 方法的一个变体接收一个 <xref:System.Drawing.Pen> 对象和四个整数，而 <xref:System.Drawing.Graphics.DrawLine%2A> 方法的另一个变体接收一个 <xref:System.Drawing.Pen> 对象和两个 <xref:System.Drawing.Point> 对象。  
  
 绘制直线、矩形和贝塞尔样条的方法具有多个伴随方法，可在一个调用中绘制若干个项：<xref:System.Drawing.Graphics.DrawLines%2A>、<xref:System.Drawing.Graphics.DrawRectangles%2A> 和 <xref:System.Drawing.Graphics.DrawBeziers%2A>。  <xref:System.Drawing.Graphics.DrawCurve%2A> 方法也有一个伴随方法 <xref:System.Drawing.Graphics.DrawClosedCurve%2A>，该伴随方法能够通过连接曲线的终点和起点的方式来闭合曲线。  
  
 <xref:System.Drawing.Graphics> 类的所有绘制方法与 <xref:System.Drawing.Pen> 对象共同工作。  若要进行绘制，必须至少创建两个对象：<xref:System.Drawing.Graphics> 对象和 <xref:System.Drawing.Pen> 对象。  <xref:System.Drawing.Pen> 对象存储要绘制项的特性，如线宽和颜色。  将 <xref:System.Drawing.Pen> 对象作为参数之一传递给绘制方法。  例如，下面的示例演示 <xref:System.Drawing.Graphics.DrawLine%2A> 方法的一个变体接收一个 <xref:System.Drawing.Pen> 对象和四个整数，并绘制一个宽 100、高 50 且左上角位于 \(20, 10\) 的矩形：  
  
 [!code-csharp[LinesCurvesAndShapes#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#11)]
 [!code-vb[LinesCurvesAndShapes#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#11)]  
  
## 请参阅  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [如何：创建用于绘制的 Graphics 对象](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)