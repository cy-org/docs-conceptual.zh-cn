---
title: "如何：用 GDI 绘制文本 | Microsoft Docs"
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
  - "绘图, 文本"
  - "GDI, 绘制文本 [Windows 窗体]"
  - "文本, 使用 TextRenderer 绘制"
  - "Windows 窗体, 使用 GDI 绘制文本"
ms.assetid: 2a19fe5d-2ace-451c-94db-01cb1118ef7b
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：用 GDI 绘制文本
使用 <xref:System.Windows.Forms.TextRenderer> 类中的 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 方法，可以访问用于在窗体或控件上绘制文本的 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 功能。  [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 文本呈现通常提供比 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 更好的性能和更精确的文本测量。  
  
> [!NOTE]
>  不支持 <xref:System.Windows.Forms.TextRenderer> 类的 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 方法进行打印。  在打印时，总是使用 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawString%2A> 方法。  
  
## 示例  
 下面的代码示例演示如何使用 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 方法在矩形内以多行形式绘制文本。  
  
 [!code-csharp[System.Windows.Forms.TextRendererExamples#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.TextRendererExamples/CS/Form1.cs#7)]
 [!code-vb[System.Windows.Forms.TextRendererExamples#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.TextRendererExamples/VB/Form1.vb#7)]  
  
 若要用 <xref:System.Windows.Forms.TextRenderer> 类呈现文本，需要 <xref:System.Drawing.IDeviceContext>（如 <xref:System.Drawing.Graphics> 和 <xref:System.Drawing.Font>）、绘制文本的位置和应该用于绘制文本的颜色。  还可以使用 <xref:System.Windows.Forms.TextFormatFlags> 枚举指定文本格式设置。  
  
 有关如何获取 <xref:System.Drawing.Graphics> 的更多信息，请参见 [如何：创建用于绘制的 Graphics 对象](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)。  有关如何构造 <xref:System.Drawing.Font> 的更多信息，请参见 [如何：构造字体系列和字体](../../../../docs/framework/winforms/advanced/how-to-construct-font-families-and-fonts.md)。  
  
## 编译代码  
 前面的代码示例旨在用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 <xref:System.Windows.Forms.TextRenderer>   
 <xref:System.Drawing.Font>   
 <xref:System.Drawing.Color>   
 <xref:System.Drawing.Color>   
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)