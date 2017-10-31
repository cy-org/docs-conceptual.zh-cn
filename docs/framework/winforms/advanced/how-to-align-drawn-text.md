---
title: "如何：对齐绘制的文本 | Microsoft Docs"
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
  - "文本, 对齐"
  - "Windows 窗体, 对齐绘制的文本"
ms.assetid: 83c10a81-1a90-4b5c-98aa-2c6c4b280079
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：对齐绘制的文本
执行自定义绘制时，您可能常常希望在窗体或控件中使绘制的文本居中。  通过创建正确的格式设置对象和设置适当的格式标志，可以轻松地对齐用 <xref:System.Drawing.Graphics.DrawString%2A> 或 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 方法绘制的文本。  
  
### 用 GDI\+ \(DrawString\) 绘制居中文本  
  
1.  将 <xref:System.Drawing.StringFormat> 与适当的 <xref:System.Drawing.Graphics.DrawString%2A> 方法一起使用以指定居中文本。  
  
     [!code-csharp[System.Drawing.AlignDrawnText#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#10)]
     [!code-vb[System.Drawing.AlignDrawnText#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#10)]  
  
### 用 GDI \(DrawText\) 绘制居中文本  
  
1.  将 <xref:System.Windows.Forms.TextFormatFlags> 枚举与适当的 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 方法一起使用以进行换行以及使文本垂直和水平居中。  
  
     [!code-csharp[System.Drawing.AlignDrawnText#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#20)]
     [!code-vb[System.Drawing.AlignDrawnText#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#20)]  
  
## 编译代码  
 前面的代码示例旨在用于 Windows 窗体，这些示例需要作为 <xref:System.Windows.Forms.PaintEventHandler> 参数的 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [如何：用 GDI 绘制文本](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)   
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [如何：构造字体系列和字体](../../../../docs/framework/winforms/advanced/how-to-construct-font-families-and-fonts.md)