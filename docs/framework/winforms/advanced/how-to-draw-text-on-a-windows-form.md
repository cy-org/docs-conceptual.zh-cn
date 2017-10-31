---
title: "如何：在 Windows 窗体上绘制文本 | Microsoft Docs"
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
  - "窗体, 绘制文本"
  - "文本, 绘图"
ms.assetid: 5d2447a9-21a1-4adc-b954-5516f2bb9b2c
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：在 Windows 窗体上绘制文本
下面的代码示例演示如何使用 <xref:System.Drawing.Graphics> 的 <xref:System.Drawing.Graphics.DrawString%2A> 方法在窗体上绘制文本。  或者，可以使用 <xref:System.Windows.Forms.TextRenderer> 在窗体上绘制文本。  有关更多信息，请参见 [如何：用 GDI 绘制文本](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)。  
  
## 示例  
 [!code-cpp[System.Drawing.ConceptualHowTos#7](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#7)]
 [!code-csharp[System.Drawing.ConceptualHowTos#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#7)]
 [!code-vb[System.Drawing.ConceptualHowTos#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#7)]  
  
## 编译代码  
 不能在 <xref:System.Windows.Forms.Form.Load> 事件处理程序中调用 <xref:System.Drawing.Graphics.DrawString%2A> 方法。  如果已调整该窗体的大小或者其他窗体遮蔽了该窗体，则不会重绘所绘制的内容。  若要自动重绘内容，应该重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   未安装 Arial 字体。  
  
## 请参阅  
 <xref:System.Drawing.Graphics.DrawString%2A>   
 <xref:System.Windows.Forms.TextRenderer.DrawText%2A>   
 <xref:System.Drawing.StringFormat.FormatFlags%2A>   
 <xref:System.Drawing.StringFormatFlags>   
 <xref:System.Windows.Forms.TextFormatFlags>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 [图形编程入门](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [如何：用 GDI 绘制文本](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)