---
title: "如何：联接线条 | Microsoft Docs"
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
  - "斜角线段联接样式"
  - "绘图, 联接线条"
  - "图形, 联接线条"
  - "GraphicsPath 对象"
  - "线条联接"
  - "文本行, 联接"
  - "斜角线段联接样式"
  - "Pen 类"
  - "圆角线段联接样式"
ms.assetid: 9fc480c2-3c75-4fd1-8ab5-296a99e820e2
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：联接线条
线条联接点是由两条端点相交或重叠的线条构成的共同区域。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供了三种线条联接样式：斜接、斜切和圆。  线条联接样式是 <xref:System.Drawing.Pen> 类的一个属性。  当为 <xref:System.Drawing.Pen> 对象指定线条联接样式时，联接样式将应用到任何使用该笔绘制的 <xref:System.Drawing.Drawing2D.GraphicsPath> 对象中的所有连接线条。  
  
 下面的插图演示产生的斜切线条联接的结果。  
  
 ![钢笔](../../../../docs/framework/winforms/advanced/media/pens5.png "pens5")  
  
## 示例  
 可通过使用 <xref:System.Drawing.Pen> 类的 <xref:System.Drawing.Pen.LineJoin%2A> 属性指定线条联接样式。  下面的示例演示水平线条和垂直线条之间的斜切线条联接。  在下面的代码中，赋给 <xref:System.Drawing.Pen.LineJoin%2A> 属性的值 <xref:System.Drawing.Drawing2D.LineJoin> 为 <xref:System.Drawing.Drawing2D.LineJoin> 枚举的一个成员。  <xref:System.Drawing.Drawing2D.LineJoin> 枚举的其它成员是：<xref:System.Drawing.Drawing2D.LineJoin> 和 <xref:System.Drawing.Drawing2D.LineJoin>。  
  
 [!code-csharp[System.Drawing.UsingAPen#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.UsingAPen#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#31)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)