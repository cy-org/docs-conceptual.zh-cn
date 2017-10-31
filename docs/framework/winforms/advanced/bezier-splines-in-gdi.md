---
title: "GDI+ 中的贝塞尔样条 | Microsoft Docs"
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
  - "贝塞尔曲线样条"
  - "GDI+, 贝塞尔曲线样条"
  - "样条, 贝塞尔曲线"
ms.assetid: 5774ce1e-87d4-4bc7-88c4-4862052781b8
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# GDI+ 中的贝塞尔样条
贝塞尔样条是由四个点指定的曲线：两个端点（p1 和 p2）和两个控制点（c1 和 c2）。  曲线开始于 p1，结束于 p2。  该曲线不经过控制点，但是控制点的作用像磁铁一样，在某些方向上拉拽曲线并影响曲线弯曲的方式。  下面的插图显示一个贝塞尔曲线及其端点和控制点。  
  
 ![贝塞尔样条](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art11a.png "Aboutgdip02\_art11a")  
  
 该曲线始于 p1 并向控制点 c1 移动。  该曲线 p1 处的切线是从 p1 到 c1 绘制的线。  端点 p2 处的切线为从 c2 到 p2 绘制的线。  
  
## 绘制贝塞尔样条  
 若要绘制贝塞尔样条，需要 <xref:System.Drawing.Graphics> 类的实例和 <xref:System.Drawing.Pen>。  <xref:System.Drawing.Graphics> 类的实例提供 <xref:System.Drawing.Graphics.DrawBezier%2A> 方法，而 <xref:System.Drawing.Pen> 存储用于呈现曲线的线的特性，如宽度和颜色。  将 <xref:System.Drawing.Pen> 作为参数之一传递给 <xref:System.Drawing.Graphics.DrawBezier%2A> 方法。  传递给 <xref:System.Drawing.Graphics.DrawBezier%2A> 方法的其他参数是端点和控制点。  下面的示例绘制了一个贝塞尔样条：起点为 \(0, 0\)，控制点为 \(40, 20\) 和 \(80, 150\)，终点为 \(100, 10\)：  
  
 [!code-csharp[LinesCurvesAndShapes#71](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#71)]
 [!code-vb[LinesCurvesAndShapes#71](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#71)]  
  
 下面的插图显示了曲线、控制点和两条切线。  
  
 ![贝塞尔样条](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art12.png "Aboutgdip02\_art12")  
  
 贝塞尔样条最初是由 Pierre Bézier 为汽车行业设计而提出的。  许多类型的计算机辅助设计都证明了它们十分有用，它们也用于定义字体的轮廓。  贝塞尔样条可生成各种各样的形状，下面的插图显示了其中的一部分。  
  
 ![路径](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art13.png "Aboutgdip02\_art13")  
  
## 请参阅  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [构造并绘制曲线](../../../../docs/framework/winforms/advanced/constructing-and-drawing-curves.md)   
 [如何：创建用于绘制的 Graphics 对象](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [如何：创建钢笔](../../../../docs/framework/winforms/advanced/how-to-create-a-pen.md)