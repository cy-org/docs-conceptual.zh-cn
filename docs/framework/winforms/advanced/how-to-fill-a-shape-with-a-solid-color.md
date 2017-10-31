---
title: "如何：用纯色填充形状 | Microsoft Docs"
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
  - "颜色, 添加到形状"
  - "形状, 填充"
ms.assetid: 06088b31-bac9-4ef3-9ebe-06c2c764d6df
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：用纯色填充形状
若要用纯色填充形状，请创建 <xref:System.Drawing.SolidBrush> 对象，然后将该 <xref:System.Drawing.SolidBrush> 对象作为一个参数传递给 <xref:System.Drawing.Graphics> 类的某个填充方法。  下面的示例演示如何用红色填充椭圆。  
  
## 示例  
 在下面的代码中，<xref:System.Drawing.SolidBrush.%23ctor%2A> 构造函数采用一个 <xref:System.Drawing.Color> 对象作为其仅有的参数。  <xref:System.Drawing.Color.FromArgb%2A> 方法使用的值分别表示颜色的 alpha、红色、绿色和蓝色分量。  这些值中的每一个都必须在 0 到 255 之间。  第一个 255 表示颜色是完全不透明的，第二个 255 表示红色分量的强度达到最大。  两个零表示绿色和蓝色分量的强度为 0。  
  
 传递给 <xref:System.Drawing.Graphics.FillEllipse%2A> 方法的四个数 \(0, 0, 100, 60\) 指定该椭圆的外接矩形的位置和尺寸。  该矩形的左上角位于 \(0, 0\)，宽度为 100，高度为 60。  
  
 [!code-csharp[System.Drawing.UsingABrush#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.UsingABrush#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#11)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [使用画笔填充形状](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)