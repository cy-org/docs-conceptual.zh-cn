---
title: "在 GDI+ 中绘制、定位和克隆图像 | Microsoft Docs"
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
  - "绘图, 图像"
  - "绘图, 光栅图像"
  - "GDI+, 克隆图像"
  - "GDI+, 绘制图像"
  - "GDI+, 定位图像"
  - "图像 [Windows 窗体], 克隆"
  - "图像 [Windows 窗体], 绘图"
  - "图像 [Windows 窗体], 定位"
  - "光栅图像"
ms.assetid: 09f0c07a-19c0-43b4-90a2-862a10545ce8
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 在 GDI+ 中绘制、定位和克隆图像
可以使用 <xref:System.Drawing.Bitmap> 类加载和显示光栅图像，还可利用 <xref:System.Drawing.Imaging.Metafile> 类加载和显示矢量图像。  <xref:System.Drawing.Bitmap> 类和 <xref:System.Drawing.Imaging.Metafile> 类从 <xref:System.Drawing.Image> 类继承。  若要显示矢量图像，需要 <xref:System.Drawing.Graphics> 类的实例和 <xref:System.Drawing.Imaging.Metafile>。  若要显示光栅图像，则需要 <xref:System.Drawing.Graphics> 类的实例和 <xref:System.Drawing.Bitmap>。  <xref:System.Drawing.Graphics> 类的实例提供了 <xref:System.Drawing.Graphics.DrawImage%2A> 方法，该方法接收 <xref:System.Drawing.Imaging.Metafile> 或 <xref:System.Drawing.Bitmap> 作为参数。  
  
## 文件类型和克隆  
 下面的代码示例演示如何用文件 Climber.jpg 构造 <xref:System.Drawing.Bitmap>，并显示位图。  图像左上角的目标点 \(10，10\) 在第二个和第三个参数中指定。  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#11)]  
  
 下面的插图显示了该图像。  
  
 ![图像示例](../../../../docs/framework/winforms/advanced/media/aboutgdip03-art04.png "AboutGdip03\_Art04")  
  
 可以用各种图形文件格式（BMP、GIF、JPEG、EXIF、PNG、TIFF 和 ICON）构造 <xref:System.Drawing.Bitmap> 对象。  
  
 下面的代码示例演示如何使用各种文件类型构造 <xref:System.Drawing.Bitmap> 对象，并显示位图。  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#12)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#12)]  
  
 <xref:System.Drawing.Bitmap> 类提供了 <xref:System.Drawing.Bitmap.Clone%2A> 方法，可用于制作现有 <xref:System.Drawing.Bitmap> 的副本。  <xref:System.Drawing.Bitmap.Clone%2A> 方法带有源矩形参数，可用于指定要复制的原始位图的部分。  下面的代码示例演示如何利用克隆现有 <xref:System.Drawing.Bitmap> 的上半部创建 <xref:System.Drawing.Bitmap>。  然后绘制两幅图像。  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#13](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#13)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#13](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#13)]  
  
 下面的插图显示这两幅图像。  
  
 ![裁剪](../../../../docs/framework/winforms/advanced/media/aboutgdip03-art05.png "AboutGdip03\_Art05")  
  
## 请参阅  
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [如何：创建用于绘制的 Graphics 对象](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [使用图像、位图、图标和图元文件](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)