---
title: "如何：对文本使用抗锯齿效果 | Microsoft Docs"
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
  - "Antialias 处理, 使用文本"
  - "字符串 [Windows 窗体], 绘制时进行 Antialias 处理"
  - "字符串 [Windows 窗体], 平滑绘制"
  - "文本 [Windows 窗体], Antialias 处理"
  - "文本 [Windows 窗体], 平滑"
ms.assetid: 48fc34f3-f236-4b01-a0cb-f0752e6d22ae
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：对文本使用抗锯齿效果
“抗锯齿”是指对绘制的图形和文本的粗糙边缘进行平滑处理以改进它们的外观或可读性。  通过托管 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 类，既可以呈现高质量的抗锯齿的文本，也可以呈现低质量文本。  通常，呈现的质量越高，所需的处理时间越长。  若要设置文本的质量级别，请将 <xref:System.Drawing.Graphics> 的 <xref:System.Drawing.Graphics.TextRenderingHint%2A> 属性设置为 <xref:System.Drawing.Text.TextRenderingHint> 枚举元素之一  
  
## 示例  
 下面的代码示例以两种不同的质量设置绘制文本：  
  
 下面的插图显示修改后的代码示例的输出。  
  
 ![字体文本](../../../../docs/framework/winforms/advanced/media/fontstext10.png "FontsText10")  
  
 [!code-csharp[System.Drawing.FontsAndText#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.FontsAndText#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#21)]  
  
## 编译代码  
 前面的代码示例是为用于 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)