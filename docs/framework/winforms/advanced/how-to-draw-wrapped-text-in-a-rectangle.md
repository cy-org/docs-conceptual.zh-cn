---
title: "如何：在矩形中绘制换行文本 | Microsoft Docs"
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
  - "字符串 [Windows 窗体], 在矩形中绘制"
  - "文本 [Windows 窗体], 在矩形中绘制"
  - "Windows 窗体, 在矩形中绘制文本"
ms.assetid: e1fb432a-dc90-48b5-9b6b-acc14507133d
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：在矩形中绘制换行文本
可以使用 <xref:System.Drawing.Graphics> 类的接受 <xref:System.Drawing.Rectangle> 或 <xref:System.Drawing.RectangleF> 参数的 <xref:System.Drawing.Graphics.DrawString%2A> 重载方法在矩形中绘制换行文本。  您还将使用 <xref:System.Drawing.Brush> 和 <xref:System.Drawing.Font>。  
  
 也可以使用 <xref:System.Windows.Forms.TextRenderer> 的接受 <xref:System.Drawing.Rectangle> 和 <xref:System.Windows.Forms.TextFormatFlags> 参数的 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 重载方法在矩形中绘制换行文本。  您还将使用 <xref:System.Drawing.Color> 和 <xref:System.Drawing.Font>。  
  
 下图显示使用 <xref:System.Drawing.Graphics.DrawString%2A> 方法时在矩形中绘制的文本的输出。  
  
 ![字体文本](../../../../docs/framework/winforms/advanced/media/csfontstext2.png "csfontstext2")  
  
### 用 GDI\+ 在矩形中绘制换行文本  
  
1.  使用 <xref:System.Drawing.Graphics.DrawString%2A> 重载方法，使用时传入您需要的文本、<xref:System.Drawing.Rectangle> 或 <xref:System.Drawing.RectangleF>、<xref:System.Drawing.Font> 以及 <xref:System.Drawing.Brush>。  
  
     [!code-csharp[System.Drawing.AlignDrawnText#50](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#50)]
     [!code-vb[System.Drawing.AlignDrawnText#50](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#50)]  
  
### 用 GDI 在矩形中绘制换行文本  
  
1.  使用 <xref:System.Windows.Forms.TextFormatFlags> 枚举值指定应通过 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 重载方法换行的文本，使用时传入您需要的文本、<xref:System.Drawing.Rectangle>、<xref:System.Drawing.Font> 以及 <xref:System.Drawing.Color>。  
  
     [!code-csharp[System.Drawing.AlignDrawnText#60](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#60)]
     [!code-vb[System.Drawing.AlignDrawnText#60](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#60)]  
  
## 编译代码  
 前面的示例需要：  
  
-   <xref:System.Windows.Forms.PaintEventArgs> `e`，它是 <xref:System.Windows.Forms.PaintEventHandler> 的一个参数。  
  
## 请参阅  
 [如何：用 GDI 绘制文本](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)   
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [如何：构造字体系列和字体](../../../../docs/framework/winforms/advanced/how-to-construct-font-families-and-fonts.md)   
 [如何：在指定位置绘制文本](../../../../docs/framework/winforms/advanced/how-to-draw-text-at-a-specified-location.md)