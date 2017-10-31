---
title: "如何：在 Windows 窗体上绘制实心椭圆 | Microsoft Docs"
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
  - "Graphics.FillEllipse"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "圆形, 绘图"
  - "环形形状"
  - "绘图, 椭圆"
  - "椭圆, 绘图"
  - "窗体, 绘制椭圆"
  - "形状, 绘图"
ms.assetid: 781db806-950d-4c5b-b022-493f7fd0c4a8
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：在 Windows 窗体上绘制实心椭圆
此示例在窗体上绘制实心椭圆。  
  
## 示例  
 [!code-cpp[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#1)]
 [!code-csharp[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#1)]
 [!code-vb[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#1)]  
  
## 编译代码  
 不能在 <xref:System.Windows.Forms.Form.Load> 事件处理程序中调用此方法。  如果已调整该窗体的大小或者其他窗体遮蔽了该窗体，则不会重绘所绘制的内容。  若要自动重绘内容，应该重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。  
  
## 可靠编程  
 对任何消耗系统资源的对象（如 <xref:System.Drawing.Brush> 和 <xref:System.Drawing.Graphics> 对象）都应调用 <xref:System.IDisposable.Dispose%2A>。  
  
## 请参阅  
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [图形编程入门](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Alpha 混合线条和填充](../../../../docs/framework/winforms/advanced/alpha-blending-lines-and-fills.md)   
 [使用画笔填充形状](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)