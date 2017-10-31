---
title: "如何：使用钢笔绘制矩形 | Microsoft Docs"
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
  - "钢笔, 绘制矩形"
  - "矩形, 绘图"
ms.assetid: 54a7fa14-3ad8-4d64-b424-2a12005b250c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用钢笔绘制矩形
若要绘制矩形，需要 <xref:System.Drawing.Graphics> 对象和 <xref:System.Drawing.Pen> 对象。  <xref:System.Drawing.Graphics> 对象提供 <xref:System.Drawing.Graphics.DrawRectangle%2A> 方法，而 <xref:System.Drawing.Pen> 对象则存储线条的特征，如颜色和宽度。  
  
## 示例  
 下面的示例绘制一个左上角位于 \(10, 10\) 的矩形。  该矩形的宽度为 100，高度为 50。  传递给 <xref:System.Drawing.Pen.%23ctor%2A> 构造函数的第二个参数指示钢笔的宽度为 5 个像素。  
  
 绘制该矩形时，钢笔以矩形边界为中心线居中。  因为钢笔的宽度是 5，矩形的边被绘制为 5 个像素宽，因此 1 个像素绘制在边界本身，2 个像素绘制在内侧，2 个像素绘制在外侧。  有关钢笔对齐方式的详细信息，请参见[如何：设置钢笔的宽度和对齐方式](../../../../docs/framework/winforms/advanced/how-to-set-pen-width-and-alignment.md)。  
  
 下面的插图显示结果矩形。  虚线表明当钢笔的宽度为 1 个像素时矩形被绘制的位置。  矩形左上角的放大视图显示黑色粗线条以这些虚线为中心线居中。  
  
 ![钢笔](../../../../docs/framework/winforms/advanced/media/pens1.png "pens1")  
  
 [!code-csharp[System.Drawing.UsingAPen#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.UsingAPen#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#21)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)