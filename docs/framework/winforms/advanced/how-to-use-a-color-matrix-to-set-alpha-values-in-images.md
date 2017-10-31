---
title: "如何：使用颜色矩阵设置图像中的 Alpha 值 | Microsoft Docs"
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
  - "位图 [Windows 窗体], 使用颜色矩阵获得半透明"
  - "图像 [Windows 窗体], 使用颜色矩阵获得半透明"
  - "矩阵, alpha "
  - "透明度, 颜色矩阵"
ms.assetid: a27121e6-f7e9-4c09-84e2-f05aa9d2a1bb
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用颜色矩阵设置图像中的 Alpha 值
<xref:System.Drawing.Bitmap> 类（从 <xref:System.Drawing.Image> 类继承）和 <xref:System.Drawing.Imaging.ImageAttributes> 类提供用于获取和设置像素值的函数。  可使用 <xref:System.Drawing.Imaging.ImageAttributes> 类修改整个图像的 alpha 值，或可调用 <xref:System.Drawing.Bitmap> 类的 <xref:System.Drawing.Bitmap.SetPixel%2A> 方法修改单个像素的值。  
  
## 示例  
 <xref:System.Drawing.Imaging.ImageAttributes> 类具有许多可用于在呈现过程中修改图像的属性。  在下面的示例中，<xref:System.Drawing.Imaging.ImageAttributes> 对象用于将所有的 alpha 值设置为原来的 80%。  这是通过初始化一个颜色矩阵并将矩阵中的 alpha 缩放值设置为 0.8 来实现的。  颜色矩阵的地址传递给 <xref:System.Drawing.Imaging.ImageAttributes> 对象的 <xref:System.Drawing.Imaging.ImageAttributes.SetColorMatrix%2A> 方法，而 <xref:System.Drawing.Imaging.ImageAttributes> 对象传递给 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.DrawString%2A> 方法。  
  
 在呈现过程中，位图中的各个 alpha 值被转换成它们的原始值的 80%，  这将导致与背景相混合的图像。  正如下面的插图所显示的那样，位图图像看上去是透明的；您可透过它看到纯黑的线条。  
  
 ![使用矩阵的 Alpha 混合](../../../../docs/framework/winforms/advanced/media/image2.png "image2")  
  
 当图像位于背景的白色部分之上时，图像就与白色相混合。  在图像与黑色线条的相交处，图像与黑色相混合。  
  
 [!code-csharp[System.Drawing.AlphaBlending#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.AlphaBlending#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#21)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Alpha 混合线条和填充](../../../../docs/framework/winforms/advanced/alpha-blending-lines-and-fills.md)