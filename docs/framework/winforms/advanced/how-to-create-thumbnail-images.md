---
title: "如何：创建缩略图像 | Microsoft Docs"
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
  - "图像 [Windows 窗体], 创建缩略图"
  - "缩略图图像, 创建"
ms.assetid: e956242a-1e5b-4217-a3cf-5f3fb45d00ba
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 如何：创建缩略图像
缩略图像是图像的小版本。  可通过调用 <xref:System.Drawing.Image> 对象的 <xref:System.Drawing.Image.GetThumbnailImage%2A> 方法创建缩略图像。  
  
## 示例  
 下面的示例从 JPG 文件构造 <xref:System.Drawing.Image> 对象。  原始图像的宽度为 640 像素，高度为 479 像素。  该代码创建宽度和高度均为 100 像素的缩略图像。  
  
 下面的插图显示此缩略图像。  
  
 ![缩略图像](../../../../docs/framework/winforms/advanced/media/thumbnail1.png "Thumbnail1")  
  
> [!NOTE]
>  此示例中声明了一个回调方法，但从未用到此方法。  这支持 GDI\+ 的所有版本。  
  
 [!code-csharp[System.Drawing.WorkingWithImages#71](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#71)]
 [!code-vb[System.Drawing.WorkingWithImages#71](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#71)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  若要运行此示例，请按以下步骤进行操作：  
  
1.  创建新的 Windows 窗体应用程序。  
  
2.  将代码示例添加到窗体中。  
  
3.  为窗体的 <xref:System.Windows.Forms.Control.Paint> 事件创建一个处理程序。  
  
4.  在 <xref:System.Windows.Forms.Control.Paint> 处理程序中，调用 `GetThumbnail` 方法并为 <xref:System.Windows.Forms.PaintEventArgs> 传递 `e`。  
  
5.  找到要生成其缩略图的图像文件。  
  
6.  在 `GetThumbnail` 方法中，指定图像的路径和文件名。  
  
7.  按 F5 运行示例。  
  
     一个 100 x 100 的缩略图图像出现在窗体上。  
  
## 请参阅  
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [使用图像、位图、图标和图元文件](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)