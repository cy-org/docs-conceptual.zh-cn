---
title: "如何：在指定位置绘制文本 | Microsoft Docs"
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
  - "绘制文本"
  - "绘制文本, 指定位置 [Windows 窗体]"
  - "文本, 在指定位置绘制 [Windows 窗体]"
  - "Windows 窗体, 在指定位置绘制文本"
ms.assetid: 60816423-1c38-465e-980d-2c2b64d74086
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：在指定位置绘制文本
执行自定义绘制时，您可以在从指定点开始的一个水平行上绘制文本。  可以使用 <xref:System.Drawing.Graphics> 类的接受 <xref:System.Drawing.Point> 或 <xref:System.Drawing.PointF> 参数的 <xref:System.Drawing.Graphics.DrawString%2A> 重载方法，以此种方式绘制文本。  <xref:System.Drawing.Graphics.DrawString%2A> 方法还需要 <xref:System.Drawing.Brush> 和 <xref:System.Drawing.Font>  
  
 还可以使用接受 <xref:System.Drawing.Point> 的 <xref:System.Windows.Forms.TextRenderer> 的重载方法 <xref:System.Windows.Forms.TextRenderer.DrawText%2A>。  <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 还需要 <xref:System.Drawing.Color> 和 <xref:System.Drawing.Font>。  
  
 下图显示使用 <xref:System.Drawing.Graphics.DrawString%2A> 重载方法时在指定点上绘制的文本的输出。  
  
 ![字体文本](../../../../docs/framework/winforms/advanced/media/csfontstext1.png "csfontstext1")  
  
### 用 GDI\+ 绘制一行文本  
  
1.  使用 <xref:System.Drawing.Graphics.DrawString%2A> 方法，使用时传入您需要的文本、<xref:System.Drawing.Point> 或 <xref:System.Drawing.PointF>、<xref:System.Drawing.Font> 以及 <xref:System.Drawing.Brush>。  
  
     [!code-csharp[System.Drawing.AlignDrawnText#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#30)]
     [!code-vb[System.Drawing.AlignDrawnText#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#30)]  
  
### 用 GDI 绘制一行文本  
  
1.  使用 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 方法，使用时传入所需的文本、<xref:System.Drawing.Point>、<xref:System.Drawing.Font> 以及 <xref:System.Drawing.Color>。  
  
     [!code-csharp[System.Drawing.AlignDrawnText#40](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#40)]
     [!code-vb[System.Drawing.AlignDrawnText#40](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#40)]  
  
## 编译代码  
 前面的示例需要：  
  
-   <xref:System.Windows.Forms.PaintEventArgs>  `e`，它是 <xref:System.Windows.Forms.PaintEventHandler> 的一个参数。  
  
## 请参阅  
 [如何：用 GDI 绘制文本](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)   
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [如何：构造字体系列和字体](../../../../docs/framework/winforms/advanced/how-to-construct-font-families-and-fonts.md)   
 [如何：在矩形中绘制换行文本](../../../../docs/framework/winforms/advanced/how-to-draw-wrapped-text-in-a-rectangle.md)