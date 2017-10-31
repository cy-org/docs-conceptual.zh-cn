---
title: "如何：转换图像颜色 | Microsoft Docs"
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
  - "位图 [Windows 窗体], 更改颜色"
  - "图像颜色 [Windows 窗体]"
  - "图像 [Windows 窗体], 更改颜色"
ms.assetid: 2106fb9a-4d60-4dcf-9220-9f189a6c4d19
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：转换图像颜色
平移是指在这四个颜色分量中的一个或多个中添加值。  下表给出表示平移的颜色矩阵项。  
  
|要平移的分量|矩阵项|  
|------------|---------|  
|Red|\[4\]\[0\]|  
|绿色|\[4\]\[1\]|  
|蓝色|\[4\]\[2\]|  
|Alpha|\[4\]\[3\]|  
  
## 示例  
 下面的示例从 ColorBars.bmp 文件构造一个 <xref:System.Drawing.Image> 对象。  然后，代码为图像中每个像素的红色分量增加 0.75。  原来的图像绘制在变换后的图像旁边。  
  
 下面的插图在左侧显示原来的图像，在右侧显示变换后的图像。  
  
 ![转换颜色](../../../../docs/framework/winforms/advanced/media/colortrans2.png "colortrans2")  
  
 下表列出在进行红色平移前后，四栏的颜色矢量。  请注意，因为颜色分量的最大值是 1，所以第二行中的红色分量不发生改变。  （同样，颜色分量的最小值为 0。）  
  
|Original|平移后|  
|--------------|---------|  
|黑色 \(0, 0, 0, 1\)|\(0.75, 0, 0, 1\)|  
|红色 \(1, 0, 0, 1\)|\(1, 0, 0, 1\)|  
|绿色 \(0, 1, 0, 1\)|\(0.75, 1, 0, 1\)|  
|蓝色 \(0, 0, 1, 1\)|\(0.75, 0, 1, 1\)|  
  
 [!code-csharp[System.Drawing.RecoloringImages#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.RecoloringImages#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#11)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  用系统中有效的图像文件名和路径替换 `ColorBars.bmp` 。  
  
## 请参阅  
 <xref:System.Drawing.Imaging.ColorMatrix>   
 <xref:System.Drawing.Imaging.ImageAttributes>   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [对图像重新着色](../../../../docs/framework/winforms/advanced/recoloring-images.md)