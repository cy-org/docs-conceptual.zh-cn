---
title: "如何：在 Windows 窗体上绘制垂直文本 | Microsoft Docs"
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
  - "StringFormat.FormatFlags"
  - "Graphics.DrawString"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "字符串 [Windows 窗体], 绘制垂直的"
  - "文本 [Windows 窗体], 绘图"
  - "文本 [Windows 窗体], 绘制垂直的"
  - "文本 [Windows 窗体], 垂直文本"
ms.assetid: 717a6131-00f6-4373-b574-9894e8317799
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：在 Windows 窗体上绘制垂直文本
下面的代码示例演示如何使用 <xref:System.Drawing.Graphics> 的 <xref:System.Drawing.Graphics.DrawString%2A> 方法在窗体上绘制竖排文字。  
  
## 示例  
 [!code-cpp[System.Drawing.ConceptualHowTos#8](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#8)]
 [!code-csharp[System.Drawing.ConceptualHowTos#8](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#8)]
 [!code-vb[System.Drawing.ConceptualHowTos#8](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#8)]  
  
## 编译代码  
 不能在 <xref:System.Windows.Forms.Form.Load> 事件处理程序中调用此方法。  如果已调整该窗体的大小或者其他窗体遮蔽了该窗体，则不会重绘所绘制的内容。  若要自动重绘内容，应该重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   未安装 Arial 字体。  
  
## 请参阅  
 <xref:System.Drawing.Graphics.DrawString%2A>   
 <xref:System.Drawing.StringFormat.FormatFlags%2A>   
 <xref:System.Drawing.StringFormatFlags>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 [图形编程入门](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)