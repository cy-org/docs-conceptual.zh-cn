---
title: "如何：在 Windows 窗体上绘制实心矩形 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Graphics.FillRectangle"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "绘制矩形"
  - "绘图, 矩形"
  - "矩形, 绘图"
ms.assetid: d656a93c-987d-4809-aafd-493fe17450f0
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：在 Windows 窗体上绘制实心矩形
此示例在窗体上绘制实心矩形。  
  
## 示例  
 [!code-cpp[System.Drawing.ConceptualHowTos#2](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#2)]
 [!code-csharp[System.Drawing.ConceptualHowTos#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#2)]
 [!code-vb[System.Drawing.ConceptualHowTos#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#2)]  
  
## 编译代码  
 不能在 <xref:System.Windows.Forms.Form.Load> 事件处理程序中调用此方法。  如果已调整该窗体的大小或者其他窗体遮蔽了该窗体，则不会重绘所绘制的内容。  若要自动重绘内容，应该重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。  
  
## 可靠编程  
 对任何消耗系统资源的对象（如 <xref:System.Drawing.Brush> 和 <xref:System.Drawing.Graphics> 对象）都应调用 <xref:System.IDisposable.Dispose%2A>。  
  
## 请参阅  
 <xref:System.Drawing.Graphics.FillRectangle%2A>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 [图形编程入门](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [GDI\+ 中的画笔和实心形状](../../../../docs/framework/winforms/advanced/brushes-and-filled-shapes-in-gdi.md)