---
title: "如何：使用颜色重新映射表 | Microsoft Docs"
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
  - "颜色重新映射表, using"
  - "颜色表, 重新映射颜色"
  - "自定义颜色, 使用颜色重新映射表创建"
ms.assetid: 977df1ce-8665-42d4-9fb1-ef7f0ff63419
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：使用颜色重新映射表
再变换是按照颜色再变换表变换图像中的颜色的过程。  颜色重新映射表是 <xref:System.Drawing.Imaging.ColorMap> 对象的数组。  该数组中的每个 <xref:System.Drawing.Imaging.ColorMap> 对象有一个 <xref:System.Drawing.Imaging.ColorMap.OldColor%2A> 属性和一个 <xref:System.Drawing.Imaging.ColorMap.NewColor%2A> 属性。  
  
 当 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 绘制图像时，图像的每个像素都会与旧颜色的数组进行比较。  如果像素的颜色与旧颜色相匹配，则它的颜色将更改为相应的新颜色。  只改变颜色的呈现方式，图像本身的颜色值（存储在 <xref:System.Drawing.Image> 或 <xref:System.Drawing.Bitmap> 对象中）不发生改变。  
  
 若要绘制再映射的图像，请初始化 <xref:System.Drawing.Imaging.ColorMap> 对象的数组。  将该数组传递给 <xref:System.Drawing.Imaging.ImageAttributes> 对象的 <xref:System.Drawing.Imaging.ImageAttributes.SetRemapTable%2A> 方法，然后将 <xref:System.Drawing.Imaging.ImageAttributes> 对象传递给 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.DrawImage%2A> 方法。  
  
## 示例  
 下面的示例从文件 RemapInput.bmp 创建一个 <xref:System.Drawing.Image> 对象。  该代码创建由一个 <xref:System.Drawing.Imaging.ColorMap> 对象组成的颜色重新映射表。  `ColorRemap`  对象的 <xref:System.Drawing.Imaging.ColorMap.OldColor%2A> 属性为 red，<xref:System.Drawing.Imaging.ColorMap.NewColor%2A> 属性为 blue。  图像被绘制两次，一次不进行再变换，另一次进行再变换。  再变换过程将所有的红色像素都更改为蓝色。  
  
 下面的插图在左侧显示原来的图像，在右侧显示再变换后的图像。  
  
 [!code-csharp[System.Drawing.RecoloringImages#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.RecoloringImages#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#31)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [对图像重新着色](../../../../docs/framework/winforms/advanced/recoloring-images.md)   
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)