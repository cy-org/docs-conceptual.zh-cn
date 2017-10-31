---
title: "如何：在屏幕上绘制现有位图 | Microsoft Docs"
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
  - "位图 [Windows 窗体], 在 Windows 窗体中显示"
  - "位图 [Windows 窗体], 在 Windows 窗体应用程序中加载"
  - "图像 [Windows 窗体], 在 Windows 窗体上显示"
ms.assetid: 5bc558d7-b326-4050-a834-b8600da0de95
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：在屏幕上绘制现有位图
您可以轻松地在屏幕上绘制现有的图像。  首先，需要使用采用文件名 <xref:System.Drawing.Bitmap.%23ctor%28System.String%29> 的位图构造函数创建一个 <xref:System.Drawing.Bitmap> 对象。  此构造函数接受多种不同文件格式的图像，包括 BMP、GIF、JPEG、PNG 和 TIFF。  创建 <xref:System.Drawing.Bitmap> 对象之后，将此 <xref:System.Drawing.Bitmap> 对象传递给 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.DrawImage%2A> 方法。  
  
## 示例  
 下面的示例从 JPEG 文件创建 <xref:System.Drawing.Bitmap> 对象，然后绘制该位图，其左上角位于 \(60, 10\)。  
  
 下面的插图显示在指定位置绘制的位图。  
  
 ![图像位置](../../../../docs/framework/winforms/advanced/media/csimageposition1.png "csimageposition1")  
  
 [!code-csharp[System.Drawing.WorkingWithImages#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.WorkingWithImages#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#21)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [使用图像、位图、图标和图元文件](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)