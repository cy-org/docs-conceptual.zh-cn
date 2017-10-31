---
title: "如何：对渐变应用灰度校正 | Microsoft Docs"
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
  - "渐变画刷, 灰度校正"
  - "渐变, 灰度校正"
ms.assetid: da4690e7-5fac-4fd2-b3f0-5cb35c165b92
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：对渐变应用灰度校正
可通过将渐变画笔的 <xref:System.Drawing.Drawing2D.LinearGradientBrush.GammaCorrection%2A> 属性设置为 `true` 来启用线性渐变画笔的伽玛矫正。  可通过将 <xref:System.Drawing.Drawing2D.LinearGradientBrush.GammaCorrection%2A> 属性设置为 `false` 来禁用伽玛矫正。  在默认情况下，禁用伽玛矫正。  
  
## 示例  
 下面的示例创建一个线性渐变画笔并使用它填充两个矩形。  第一个矩形在填充时未启用伽玛矫正；第二个矩形在填充时启用了伽玛矫正。  
  
 下面的插图显示这两个实心矩形。  上面的矩形未采用伽玛矫正，它的中间部分看上去较暗。  下面的矩形采用了伽玛矫正，看上去亮度更均匀。  
  
 ![渐变](../../../../docs/framework/winforms/advanced/media/gammagradient1.png "gammagradient1")  
  
 [!code-csharp[System.Drawing.UsingaGradientBrush#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.UsingaGradientBrush#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#31)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 <xref:System.Drawing.Drawing2D.LinearGradientBrush>   
 [使用渐变画笔填充形状](../../../../docs/framework/winforms/advanced/using-a-gradient-brush-to-fill-shapes.md)