---
title: "使用转换来调整颜色 | Microsoft Docs"
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
  - "颜色, 缩放"
  - "转换, 用于调整颜色比例"
ms.assetid: df23c887-7fd6-4b15-ad94-e30b5bd4b849
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 使用转换来调整颜色
缩放变换是指用一个数字与这四个颜色分量中的一个或多个相乘。  下表给出表示缩放的颜色矩阵项。  
  
|要缩放的分量|矩阵项|  
|------------|---------|  
|Red|\[0\]\[0\]|  
|绿色|\[1\]\[1\]|  
|蓝色|\[2\]\[2\]|  
|Alpha|\[3\]\[3\]|  
  
## 缩放一种颜色  
 下面的示例从文件 ColorBars2.bmp 构造一个 <xref:System.Drawing.Image> 对象。  然后，代码将图像中每个像素的蓝色分量乘以 2。  原来的图像绘制在变换后的图像旁边。  
  
 [!code-csharp[System.Drawing.RecoloringImages#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.RecoloringImages#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#41)]  
  
 下面的插图在左侧显示原来的图像，在右侧显示缩放后的图像。  
  
 ![按比例调整颜色](../../../../docs/framework/winforms/advanced/media/colortrans3.png "colortrans3")  
  
 下表列出在进行蓝色缩放前后，四栏的颜色矢量。  请注意，第四个颜色栏中的蓝色分量从 0.8 变到 0.6。  这是因为 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 只保留结果的小数部分。  例如，\(2\)\(0.8\) \= 1.6，1.6 的小数部分是 0.6。  只保留小数部分可确保结果总是在 \[0, 1\] 之间。  
  
|Original|缩放后|  
|--------------|---------|  
|\(0.4, 0.4, 0.4, 1\)|\(0.4, 0.4, 0.8, 1\)|  
|\(0.4, 0.2, 0.2, 1\)|\(0.4, 0.2, 0.4, 1\)|  
|\(0.2, 0.4, 0.2, 1\)|\(0.2, 0.4, 0.4, 1\)|  
|\(0.4, 0.4, 0.8, 1\)|\(0.4, 0.4, 0.6, 1\)|  
  
## 缩放多种颜色  
 下面的示例从文件 ColorBars2.bmp 构造一个 <xref:System.Drawing.Image> 对象。  然后，该代码缩放图像中每个像素的红色、绿色和蓝色分量。  红色分量缩小了 25%，绿色分量缩小了 35%，蓝色分量缩小了 50%。  
  
 [!code-csharp[System.Drawing.RecoloringImages#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#42)]
 [!code-vb[System.Drawing.RecoloringImages#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#42)]  
  
 下面的插图在左侧显示原来的图像，在右侧显示缩放后的图像。  
  
 ![按比例调整颜色](../../../../docs/framework/winforms/advanced/media/colortrans4.png "colortrans4")  
  
 下表列出在缩放红色、绿色和蓝色前后，四栏的颜色矢量。  
  
|Original|缩放后|  
|--------------|---------|  
|\(0.6, 0.6, 0.6, 1\)|\(0.45, 0.39, 0.3, 1\)|  
|\(0, 1, 1, 1\)|\(0, 0.65, 0.5, 1\)|  
|\(1, 1, 0, 1\)|\(0.75, 0.65, 0, 1\)|  
|\(1, 0, 1, 1\)|\(0.75, 0, 0.5, 1\)|  
  
## 请参阅  
 <xref:System.Drawing.Imaging.ColorMatrix>   
 <xref:System.Drawing.Imaging.ImageAttributes>   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [对图像重新着色](../../../../docs/framework/winforms/advanced/recoloring-images.md)