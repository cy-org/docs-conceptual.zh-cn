---
title: "如何：用阴影图案填充形状 | Microsoft Docs"
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
  - "画笔, 使用阴影画笔"
  - "patterns, 添加到形状"
  - "形状, 使用图案填充"
ms.assetid: 9c8300ff-187b-404f-af1f-ebd499f5b16f
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：用阴影图案填充形状
阴影图案由两种颜色组成：一种是背景色，一种是在背景上形成图案的线条的颜色。  若要用阴影图案填充闭合的形状，请使用 <xref:System.Drawing.Drawing2D.HatchBrush> 对象。  下面的示例演示如何用阴影图案填充椭圆：  
  
## 示例  
 <xref:System.Drawing.Drawing2D.HatchBrush.%23ctor%2A> 构造函数带有三个参数：阴影样式、阴影线颜色和背景颜色。  阴影样式参数可以为 <xref:System.Drawing.Drawing2D.HatchStyle> 枚举中的任何值。  在 <xref:System.Drawing.Drawing2D.HatchStyle> 枚举中有 50 多个元素；在下面的列表中显示了其中的几个元素：  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
 下面的插图显示已填充的椭圆。  
  
 ![阴影图案](../../../../docs/framework/winforms/advanced/media/hatch1.png "hatch1")  
  
 [!code-csharp[System.Drawing.UsingABrush#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.UsingABrush#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#41)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [使用画笔填充形状](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)