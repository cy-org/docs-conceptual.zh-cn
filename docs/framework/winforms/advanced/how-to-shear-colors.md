---
title: "如何：修剪颜色 | Microsoft Docs"
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
  - "颜色, 修剪"
  - "颜色, 使用颜色矩阵转换"
ms.assetid: 0a424171-5b8b-45c4-afef-e9720a6c3e22
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：修剪颜色
剪切是指按照与另一种颜色分量成比例的量来增加或减少颜色分量。  例如，考虑这样一种变换，将红色分量增加蓝色分量值的一半。  在这样的变换下，\(0.2, 0.5, 1\) 颜色将变成 \(0.7, 0.5, 1\)。  新的颜色分量是 0.2 \+ \(1\/2\)\(1\) \= 0.7。  
  
## 示例  
 下面的示例从文件 ColorBars4.bmp 构造一个 <xref:System.Drawing.Image> 对象。  然后，该代码将上一段中描述的剪切变换应用到图像中的每个像素。  
  
 下面的插图在左侧显示原来的图像，在右侧显示剪切后的图像。  
  
 ![切变颜色](../../../../docs/framework/winforms/advanced/media/colortrans6.png "colortrans6")  
  
 下表列出在剪切变换前后，四栏的颜色矢量。  
  
|Original|剪切后|  
|--------------|---------|  
|\(0, 0, 1, 1\)|\(0.5, 0, 1, 1\)|  
|\(0.5, 1, 0.5, 1\)|\(0.75, 1, 0.5, 1\)|  
|\(1, 1, 0, 1\)|\(1, 1, 0, 1\)|  
|\(0.4, 0.4, 0.4, 1\)|\(0.6, 0.4, 0.4, 1\)|  
  
 [!code-csharp[System.Drawing.Misc3#9](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Misc3/CS/Form1.cs#9)]
 [!code-vb[System.Drawing.Misc3#9](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Misc3/VB/Form1.vb#9)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  用系统上有效的图像名称和路径替换 `ColorBars.bmp`。  
  
## 请参阅  
 <xref:System.Drawing.Imaging.ColorMatrix>   
 <xref:System.Drawing.Imaging.ImageAttributes>   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [对图像重新着色](../../../../docs/framework/winforms/advanced/recoloring-images.md)