---
title: "如何：绘制空心形状 | Microsoft Docs"
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
  - "Graphics.DrawEllipse"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "圆形"
  - "圆形, 绘图"
  - "环形形状"
  - "绘图, 环形形状"
  - "绘图, 形状"
  - "椭圆, 绘图"
  - "窗体, 绘制环形形状"
  - "空心形状, 绘图"
  - "空心形状, 示例"
  - "形状, 绘图"
ms.assetid: f4f9214c-607e-407d-8cdd-6549f0278451
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：绘制空心形状
此示例在窗体上绘制空心椭圆和空心矩形。  
  
## 示例  
 [!code-cpp[System.Drawing.ConceptualHowTos#6](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#6)]
 [!code-csharp[System.Drawing.ConceptualHowTos#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#6)]
 [!code-vb[System.Drawing.ConceptualHowTos#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#6)]  
  
## 编译代码  
 不能在 <xref:System.Windows.Forms.Form.Load> 事件处理程序中调用此方法。  如果已调整该窗体的大小或者其他窗体遮蔽了该窗体，则不会重绘所绘制的内容。  若要自动重绘内容，应该重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。  
  
## 可靠编程  
 应该始终对使用系统资源的任何对象（如 <xref:System.Drawing.Pen> 和 <xref:System.Drawing.Graphics> 对象）调用 <xref:System.IDisposable.Dispose%2A>。  
  
## 请参阅  
 <xref:System.Drawing.Graphics.DrawEllipse%2A>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 <xref:System.Drawing.Graphics.DrawRectangle%2A>   
 [图形编程入门](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)