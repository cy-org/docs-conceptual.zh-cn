---
title: "如何：旋转颜色 | Microsoft Docs"
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
  - "颜色, 旋转"
  - "示例 [Windows 窗体], 旋转颜色"
ms.assetid: e2e4c300-159c-4f4a-9b56-103b0f7cbc05
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：旋转颜色
在四维颜色空间中进行的旋转难于可视化。  可通过固定一种颜色分量以便使旋转可视化。  假设我们同意将 alpha 分量固定在 1（完全不透明），  则可用红色、绿色和蓝色的轴形象地表示三维颜色空间，如下面的插图所示。  
  
 ![重新着色](../../../../docs/framework/winforms/advanced/media/recoloring03.gif "recoloring03")  
  
 颜色可视为 3\-D 空间中的一个点。  例如，空间中的点 \(1, 0, 0\) 表示红色，空间中的点 \(0, 1, 0\) 表示绿色。  
  
 下面的插图显示将 \(1, 0, 0\) 颜色在红色\-绿色平面中旋转 60 度后的结果。  在与红色\-绿色平面平行的平面中进行旋转可视为围绕蓝色轴旋转。  
  
 ![重新着色](../../../../docs/framework/winforms/advanced/media/recoloring04.gif "recoloring04")  
  
 下面的插图显示如何初始化颜色矩阵以围绕三个坐标轴（红色、绿色和蓝色）中的每一个进行旋转。  
  
 ![重新着色](../../../../docs/framework/winforms/advanced/media/recoloring05.gif "recoloring05")  
  
## 示例  
 下面的示例将一个使用一种颜色 \(1, 0, 0.6\) 的图像围绕蓝色轴旋转 60 度。  旋转角度在与红色\-绿色平面平行的平面上扫出。  
  
 下面的插图在左侧显示原来的图像，在右侧显示颜色旋转后的图像。  
  
 ![旋转颜色](../../../../docs/framework/winforms/advanced/media/colortrans5.png "colortrans5")  
  
 下面的插图形象地显示利用下面的代码进行的颜色旋转。  
  
 ![重新着色](../../../../docs/framework/winforms/advanced/media/recoloring06.gif "recoloring06")  
  
 [!code-csharp[System.Drawing.RotateColors#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RotateColors/CS/Form1.cs#1)]
 [!code-vb[System.Drawing.RotateColors#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RotateColors/VB/Form1.vb#1)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  以系统上的有效图像文件名称和路径替代 `RotationInput.bmp`。  
  
## 请参阅  
 <xref:System.Drawing.Imaging.ColorMatrix>   
 <xref:System.Drawing.Imaging.ImageAttributes>   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [对图像重新着色](../../../../docs/framework/winforms/advanced/recoloring-images.md)