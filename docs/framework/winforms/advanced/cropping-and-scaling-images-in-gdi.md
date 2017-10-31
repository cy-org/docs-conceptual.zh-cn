---
title: "在 GDI+ 中裁切和缩放图像 | Microsoft Docs"
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
  - "压缩数据, 图像"
  - "GDI+, 裁剪图像"
  - "GDI+, 缩放图像"
  - "图像 [Windows 窗体], 压缩"
  - "图像 [Windows 窗体], 裁剪"
  - "图像 [Windows 窗体], 展开"
  - "图像 [Windows 窗体], 缩放"
  - "矩形, 目标"
  - "矩形, source"
ms.assetid: ad5daf26-005f-45bc-a2af-e0e97777a21a
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 在 GDI+ 中裁切和缩放图像
可使用 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawImage%2A> 方法绘制和定位矢量图像和光栅图像。  <xref:System.Drawing.Graphics.DrawImage%2A> 是一个重载的方法，因此，可以有多种方式为该方法提供参数。  
  
## DrawImage 的变体  
 <xref:System.Drawing.Graphics.DrawImage%2A> 方法的一个变体接收一个 <xref:System.Drawing.Bitmap> 和一个 <xref:System.Drawing.Rectangle>。  该矩形指定了绘图操作的目标，即它指定了将要在其内绘图的矩形。  如果目标矩形的大小与原始图像的大小不同，原始图像将进行缩放，以适应目标矩形。  下面的代码示例演示如何将同一图像绘制三次：一次没有缩放，一次使用扩展，一次使用压缩：  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#31)]  
  
 下面的插图显示了这三张图片。  
  
 ![缩放](../../../../docs/framework/winforms/advanced/media/aboutgdip03-art06.png "AboutGdip03\_Art06")  
  
 <xref:System.Drawing.Graphics.DrawImage%2A> 方法的一些变体带有源矩形参数和目标矩形参数。  源矩形参数指定原始图像要绘制的部分。  目标矩形参数指定将要在其内绘制该图像指定部分的矩形。  如果目标矩形的大小与源矩形的大小不同，图片将会缩放，以适应目标矩形。  
  
 下面的代码示例演示如何用文件 Runner.jpg 构造 <xref:System.Drawing.Bitmap>。  整个图像在 \(0，0\) 处开始绘制，无缩放。  然后将该图像的一小部分绘制两次：一次使用压缩，一次使用扩展。  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#32](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#32](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#32)]  
  
 下面的插图显示了未缩放的图像，以及压缩的和扩展的图像部分。  
  
 ![裁剪和缩放](../../../../docs/framework/winforms/advanced/media/aboutgdip03-art07.png "AboutGdip03\_Art07")  
  
## 请参阅  
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [使用图像、位图、图标和图元文件](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)