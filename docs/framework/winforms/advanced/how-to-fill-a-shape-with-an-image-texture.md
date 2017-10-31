---
title: "如何：用图像纹理填充形状 | Microsoft Docs"
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
  - "位图 [Windows 窗体], 使用纹理"
  - "图像 [Windows 窗体], 使用画笔"
  - "形状, 使用图像填充"
ms.assetid: 508da5a6-2433-4d2b-9680-eaeae4e96e3b
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：用图像纹理填充形状
通过使用 <xref:System.Drawing.Image> 类和 <xref:System.Drawing.TextureBrush> 类，可用纹理填充闭合的形状。  
  
## 示例  
 下面的示例用图像填充椭圆。  该代码构造 <xref:System.Drawing.Image> 对象，然后将该 <xref:System.Drawing.Image> 对象的地址作为参数传递给 <xref:System.Drawing.TextureBrush.%23ctor%2A> 构造函数。  第三条语句缩放图像，第四条语句用缩放后图像的重复副本填充椭圆。  
  
 在下面的代码中，<xref:System.Drawing.TextureBrush.Transform%2A> 属性包含在绘制图像之前应用到该图像的转换。  假定原始图像的宽度为 640 像素，高度为 480 像素。  该转换通过设置水平和垂直缩放值将图像缩小到 75 x 75。  
  
> [!NOTE]
>  在下面的示例中，图像大小为 75 x 75、椭圆大小为 150 x 250。  因为图像比它所填充的椭圆小，所以图像平铺在椭圆上。  平铺意味着图像水平和垂直重复排列，直到到达形状的边界。  有关平铺的更多信息，请参见[如何：在形状中平铺图像](../../../../docs/framework/winforms/advanced/how-to-tile-a-shape-with-an-image.md)。  
  
 [!code-csharp[System.Drawing.UsingABrush#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.UsingABrush#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#21)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [使用画笔填充形状](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)