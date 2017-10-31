---
title: "如何：加载和显示图元文件 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 图元文件"
  - "图元文件, 显示"
ms.assetid: 60af1714-f148-4d85-a739-0557965ffa73
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：加载和显示图元文件
<xref:System.Drawing.Imaging.Metafile> 类继承自 <xref:System.Drawing.Image> 类，它提供用于记录、显示和检查矢量图像的方法。  
  
## 示例  
 若要在屏幕上显示矢量图像（图元文件），则需要 <xref:System.Drawing.Imaging.Metafile> 对象和 <xref:System.Drawing.Graphics> 对象。  将文件（或流）的名称传递给 <xref:System.Drawing.Imaging.Metafile> 构造函数。  在创建 <xref:System.Drawing.Imaging.Metafile> 对象之后，将此 <xref:System.Drawing.Imaging.Metafile> 对象传递给 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.DrawImage%2A> 方法。  
  
 下面的示例从 EMF 文件（增强型图元文件）创建 <xref:System.Drawing.Imaging.Metafile> 对象，然后绘制该图像，其左上角位于 \(60, 10\)。  
  
 下面的插图显示在指定位置绘制的图元文件。  
  
 ![图像位置](../../../../docs/framework/winforms/advanced/media/imageposition2.png "imageposition2")  
  
 [!code-csharp[System.Drawing.WorkingWithImages#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.WorkingWithImages#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#41)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [使用图像、位图、图标和图元文件](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)