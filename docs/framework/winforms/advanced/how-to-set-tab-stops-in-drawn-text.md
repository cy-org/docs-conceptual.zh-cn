---
title: "如何：在绘制的文本中设置制表位 | Microsoft Docs"
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
  - "选项卡, 绘制的文本"
  - "文本, 使用制表位绘制"
ms.assetid: 64878f98-39ba-4303-b63f-0859ab682eeb
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：在绘制的文本中设置制表位
通过调用 <xref:System.Drawing.StringFormat> 对象的 <xref:System.Drawing.StringFormat.SetTabStops%2A> 方法，然后将该 <xref:System.Drawing.StringFormat> 对象传递给 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawString%2A> 方法，可以设置文本的制表位。  
  
> [!NOTE]
>  尽管可以使用 <xref:System.Windows.Forms.TextFormatFlags?displayProperty=fullName> 标志扩展现有的制表位，但 <xref:System.Windows.Forms.TextRenderer?displayProperty=fullName> 不支持在绘制文本中添加新的制表位。  
  
## 示例  
 下面的示例在 150、250 和 350 处设置制表位。  然后，代码显示用制表符分隔的名称和测验分数的列表。  
  
 下面的插图显示用制表符分隔的文本。  
  
 ![字体文本](../../../../docs/framework/winforms/advanced/media/fontstext4.png "fontstext4")  
  
 下面的代码将两个参数传递给 <xref:System.Drawing.StringFormat.SetTabStops%2A> 方法。  第二个参数是包含制表位偏移量的数组。  传递给 <xref:System.Drawing.StringFormat.SetTabStops%2A> 的第一个参数是 0，它表明数组中的第一个偏移量从位置 0（边框的左边）测量。  
  
 [!code-csharp[System.Drawing.FontsAndText#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.FontsAndText#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#41)]  
  
## 编译代码  
  
-   前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [如何：用 GDI 绘制文本](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)