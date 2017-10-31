---
title: "如何：创建垂直文本 | Microsoft Docs"
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
  - "字符串 [Windows 窗体], 绘制垂直的"
  - "文本 [Windows 窗体], 绘制垂直的"
  - "垂直文本, 绘图"
  - "Windows 窗体, 绘制垂直文本"
ms.assetid: 50c69046-4188-47d9-b949-cc2610ffd337
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：创建垂直文本
可使用 <xref:System.Drawing.StringFormat> 对象指定在垂直方向而不是在水平方向绘制文本。  
  
## 示例  
 下面的示例将值 <xref:System.Drawing.StringFormatFlags> 赋给 <xref:System.Drawing.StringFormat> 对象的 <xref:System.Drawing.StringFormat.FormatFlags%2A> 属性。  该 <xref:System.Drawing.StringFormat> 对象被传递给 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawString%2A> 方法。  <xref:System.Drawing.StringFormatFlags> 值是 <xref:System.Drawing.StringFormatFlags> 枚举的成员。  
  
 下面的插图显示竖排文本。  
  
 ![字体文本](../../../../docs/framework/winforms/advanced/media/csfontstext5.png "csfontstext5")  
  
 [!code-csharp[System.Drawing.FontsAndText#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.FontsAndText#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#31)]  
  
## 编译代码  
  
-   前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> `e` 。  
  
## 请参阅  
 [如何：用 GDI 绘制文本](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)