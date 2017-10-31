---
title: "如何：通过对窗体和控件使用双缓冲来减少图形闪烁 | Microsoft Docs"
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
  - "DoubleBuffered 属性"
  - "闪烁, 在 Windows 窗体中减少"
  - "图形, 减少双缓冲闪烁"
ms.assetid: 91083d3a-653f-4f15-a467-0f37b2aa39d6
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：通过对窗体和控件使用双缓冲来减少图形闪烁
双缓冲使用内存缓冲区来解决由多重绘制操作造成的闪烁问题。  当启用双缓冲时，所有绘制操作首先呈现到内存缓冲区，而不是屏幕上的绘图图面。  所有绘制操作完成后，内存缓冲区直接复制到与其关联的绘图图面。  因为只在屏幕上执行一项图形操作，所以消除了与复杂绘图操作关联的图形闪烁。对于大多数应用程序而言，由 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 提供的默认双缓冲将提供最佳结果。  默认情况下，标准 Windows 窗体控件是双缓冲的。  可以通过两种方法对窗体和所创作的控件启用默认双缓冲。  一种方法是将 <xref:System.Windows.Forms.Control.DoubleBuffered%2A> 属性设置为 `true`，另一种方法是通过调用 <xref:System.Windows.Forms.Control.SetStyle%2A> 方法将 <xref:System.Windows.Forms.ControlStyles> 标志设置为 `true`。  两种方法都将为窗体或控件启用默认双缓冲并提供无闪烁的图形呈现。  建议仅对已为其编写所有呈现代码的自定义控件调用 <xref:System.Windows.Forms.Control.SetStyle%2A> 方法。  
  
 对于更多的高级双缓冲情形（如动画或高级内存管理），可以实现自己的双缓冲逻辑。  有关更多信息，请参见[如何：手动管理缓冲图形](../../../../docs/framework/winforms/advanced/how-to-manually-manage-buffered-graphics.md)。  
  
### 减少闪烁  
  
-   将 <xref:System.Windows.Forms.Control.DoubleBuffered%2A> 属性设置为 `true`。  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#31)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#31)]  
  
 \- 或 \-  
  
-   调用 <xref:System.Windows.Forms.Control.SetStyle%2A> 方法将 <xref:System.Windows.Forms.ControlStyles> 标志设置为 `true`。  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#32](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#32)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#32](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#32)]  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.DoubleBuffered%2A>   
 <xref:System.Windows.Forms.Control.SetStyle%2A>   
 [双缓冲图形](../../../../docs/framework/winforms/advanced/double-buffered-graphics.md)   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)