---
title: "如何：枚举已安装的字体 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 字体"
  - "字体, 枚举安装的"
ms.assetid: 26d74ef5-0f39-4eeb-8d20-00e66e014abe
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：枚举已安装的字体
<xref:System.Drawing.Text.InstalledFontCollection> 类继承自 <xref:System.Drawing.Text.FontCollection> 抽象基类。  可使用 <xref:System.Drawing.Text.InstalledFontCollection> 对象枚举计算机上安装的字体。  <xref:System.Drawing.Text.InstalledFontCollection> 对象的 <xref:System.Drawing.Text.FontCollection.Families%2A> 属性为一个 <xref:System.Drawing.FontFamily> 对象数组。  
  
## 示例  
 下面的示例列出计算机上安装的所有字体系列的名称。  该代码检索每个 <xref:System.Drawing.FontFamily> 对象的 <xref:System.Drawing.FontFamily.Name%2A> 属性，该属性存放在由 <xref:System.Drawing.Text.FontCollection.Families%2A> 属性返回的数组中。  检索到字体系列名称时，将它们连接起来以形成用逗号分隔的列表。  然后，<xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawString%2A> 方法在矩形中绘制此用逗号分隔的列表。  
  
 如果运行该代码示例，输出将与下面的插图所显示的情况相似。  
  
 ![已安装的字体](../../../../docs/framework/winforms/advanced/media/csfontstext6.png "csfontstext6")  
  
 [!code-csharp[System.Drawing.FontsAndText#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.FontsAndText#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#11)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  此外，您还应导入 <xref:System.Drawing.Text> 命名空间。  
  
## 请参阅  
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)