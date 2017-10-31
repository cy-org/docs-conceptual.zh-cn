---
title: "如何：裁切和缩放图像 | Microsoft Docs"
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
  - "图像 [Windows 窗体], 裁剪"
  - "图像 [Windows 窗体], 缩放"
ms.assetid: 053e3360-bca0-4b25-9afa-0e77a6f17b03
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：裁切和缩放图像
<xref:System.Drawing.Graphics> 类提供几个 <xref:System.Drawing.Graphics.DrawImage%2A> 方法，其中的某些方法包含可用于裁切和缩放图像的源矩形参数和目标矩形参数。  
  
## 示例  
 下面的示例从磁盘文件 Apple.gif 构造 <xref:System.Drawing.Image> 对象。  代码按照其原始尺寸绘制完整的苹果图像。  然后，该代码调用 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.DrawImage%2A> 方法，以便在大于原始苹果图像的目标矩形中绘制该苹果图像的一部分。  
  
 <xref:System.Drawing.Graphics.DrawImage%2A> 方法通过查看源矩形来确定要绘制苹果的哪部分，这由第三、第四、第五和第六个参数来指定。  在本例中，苹果在宽度和高度上均被裁切为原始尺寸的 75%。  
  
 <xref:System.Drawing.Graphics.DrawImage%2A> 方法通过查看目标矩形来确定在何处绘制裁切后的苹果以及裁切后的苹果大小，这由第二个参数指定。  在本例中，目标矩形在宽度和高度上都比原始图像大 30%。  
  
 下面的插图显示原始苹果和缩放、裁切后的苹果。  
  
 ![裁剪和缩放](../../../../docs/framework/winforms/advanced/media/cscropscale1.png "csCropScale1")  
  
 [!code-csharp[System.Drawing.WorkingWithImages#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.WorkingWithImages#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#11)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  确保用系统上有效的图像文件名和路径替换 `Apple.gif`。  
  
## 请参阅  
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [使用图像、位图、图标和图元文件](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)