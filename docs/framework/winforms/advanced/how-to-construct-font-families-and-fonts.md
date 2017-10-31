---
title: "如何：构造字体系列和字体 | Microsoft Docs"
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
  - "字体系列, 构造"
  - "字体, 构造"
ms.assetid: d3a4a223-9492-4b54-9afd-db1c31c3cefd
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：构造字体系列和字体
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 将字样相同但字形不同的字体分组为字体系列。  例如，Arial 字体系列中包含以下字体：  
  
-   Arial Regular  
  
-   Arial Bold  
  
-   Arial Italic  
  
-   Arial Bold Italic  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 使用四种字形构成字体系列：常规、粗体、倾斜和粗斜体。  像 *narrow* 和 *rounded* 之类的形容词不被视为字形；而是作为字体系列名的一部分。  例如，Arial Narrow 是包含以下成员的字体系列：  
  
-   Arial Narrow Regular  
  
-   Arial Narrow Bold  
  
-   Arial Narrow Italic  
  
-   Arial Narrow Bold Italic  
  
 在可以使用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 绘制文本之前，您需要构造一个 <xref:System.Drawing.FontFamily> 对象和一个 <xref:System.Drawing.Font> 对象。  <xref:System.Drawing.FontFamily> 对象指定字样（例如 Arial），而 <xref:System.Drawing.Font> 对象指定字号、字形和单位。  
  
## 示例  
 下面的示例构造一个字号为 16 像素、常规字形的 Arial 字体。  在下面的代码中，传递给 <xref:System.Drawing.Font.%23ctor%2A> 构造函数的第一个参数是 <xref:System.Drawing.FontFamily> 对象。  第二个参数指定字体的大小，其单位由第四个参数确定。  第三个参数确定字形。  
  
 <xref:System.Drawing.GraphicsUnit> 为 <xref:System.Drawing.GraphicsUnit> 枚举的一个成员，<xref:System.Drawing.FontStyle> 是 <xref:System.Drawing.FontStyle> 枚举的一个成员。  
  
 [!code-csharp[System.Drawing.FontsAndText#61](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.FontsAndText#61](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#61)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)