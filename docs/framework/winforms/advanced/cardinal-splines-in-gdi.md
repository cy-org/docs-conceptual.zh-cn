---
title: "GDI+ 中的基数样条 | Microsoft Docs"
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
  - "基本样条"
  - "GDI+, 基本样条"
  - "样条, 基本"
ms.assetid: 09b3797a-6294-422d-9adf-a5a0a7695c0c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# GDI+ 中的基数样条
基数样条是一连串单独的曲线，这些曲线连接起来形成一条较大的曲线。  样条由点的数组和张力参数指定。  基数样条平滑地经过数组中的每个点；曲线的陡度上没有尖角和突然的变化。  下面的插图显示了一组点和经过这一组点中每一点的基数样条。  
  
 ![基数样条](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art09.png "Aboutgdip02\_art09")  
  
## 物理和数学样条  
 物理样条是一块薄木片或其他有弹性的物质。  在数学样条出现之前，设计者利用物理样条绘制曲线。  设计者把样条放置在一张纸上并锚定到一组给定的点上。  然后，设计者就可以用钢笔沿样条绘制出一条曲线。  一组给定的点可以产生各种各样的曲线，这取决于物理样条的属性。  例如，极不易弯曲的样条与非常有弹性的样条产生的曲线是不同的。  
  
 数学样条的公式基于弹性棒条的属性，因此数学样条产生的曲线与物理样条曾产生的曲线是相同的。  正如不同张力的物理样条通过一组给定的点将产生不同的曲线一样，张力参数值不同的数学样条在一组给定的点上将产生不同的曲线。  下面的插图显示了经过同一组点的四个基数样条。  每个样条都显示了张力。  0 张力相当于无穷的物理张力，以强制曲线在点与点之间采取最短的路径（直线）。  张力为 1 对应于没有物理张力，使样条采用最小完全弯曲的路径。  张力值大于 1 的曲线就像压缩的弹簧，被挤压着采用较长的路径。  
  
 ![基数样条](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art10.png "Aboutgdip02\_art10")  
  
 上面插图中的四个样条共享起点处的同一条切线。  该切线是从起始点到沿着曲线的下一点绘制的一条线。  同样，在结束点处共享的切线是从结束点到沿着曲线的上一点绘制的一条线。  
  
 若要绘制基数样条，需要 <xref:System.Drawing.Graphics> 类的实例、<xref:System.Drawing.Pen> 和 <xref:System.Drawing.Point> 对象数组。<xref:System.Drawing.Graphics> 类的实例提供了 <xref:System.Drawing.Graphics.DrawCurve%2A> 方法以用于绘制样条，而 <xref:System.Drawing.Pen> 存储样条的特性（如线宽和颜色）。  <xref:System.Drawing.Point> 对象数组存储曲线将要经过的点。  下面的代码示例演示如何绘制经过  `myPointArray` 中的点的基数样条。  第三个参数是张力。  
  
 [!code-csharp[LinesCurvesAndShapes#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#31)]
 [!code-vb[LinesCurvesAndShapes#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#31)]  
  
## 请参阅  
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [构造并绘制曲线](../../../../docs/framework/winforms/advanced/constructing-and-drawing-curves.md)