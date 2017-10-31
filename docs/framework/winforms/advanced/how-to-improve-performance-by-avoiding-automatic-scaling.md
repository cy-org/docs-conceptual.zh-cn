---
title: "如何：通过避免自动缩放改善性能 | Microsoft Docs"
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
  - "自动缩放"
  - "图像 [Windows 窗体], 改善性能"
  - "图像 [Windows 窗体], 在使用时不进行自动缩放"
  - "性能, 改善图像"
ms.assetid: 5fe2c95d-8653-4d55-bf0d-e5afa28f223b
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：通过避免自动缩放改善性能
在绘制图像时，[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 可能会自动缩放图像，这将会导致性能降低。  另外，也可以通过将目标矩形的尺寸传递给 <xref:System.Drawing.Graphics.DrawImage%2A> 方法来控制图像的缩放。  
  
 例如，以下对 <xref:System.Drawing.Graphics.DrawImage%2A> 方法的调用指定左上角的位置为 \(50, 30\)，但是未指定目标矩形。  
  
 [!code-csharp[System.Drawing.WorkingWithImages#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.WorkingWithImages#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#31)]  
  
 尽管从所需参数的数量上来说，这是 <xref:System.Drawing.Graphics.DrawImage%2A> 方法最方便的版本，但它不一定是最有效的。  如果 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 使用的分辨率（通常是 96 点\/英寸）与 <xref:System.Drawing.Image> 对象中存储的分辨率不同，则 <xref:System.Drawing.Graphics.DrawImage%2A> 方法将缩放图像。  例如，假定一个 <xref:System.Drawing.Image> 对象的宽度为 216 像素而存储的水平分辨率值为 72 点\/英寸。  因为 216 除以 72 等于 3，所以 <xref:System.Drawing.Graphics.DrawImage%2A> 将缩放该图像，使其在 96 点\/英寸的分辨率下的宽度为 3 英寸。  也就是说，<xref:System.Drawing.Graphics.DrawImage%2A> 将显示一个宽度为 96x3 \= 288 像素的图像。  
  
 即使您的屏幕分辨率不是 96 点\/英寸，[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 也可能会像屏幕分辨率是 96 点\/英寸那样缩放图像。  这是因为 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] <xref:System.Drawing.Graphics> 对象是与设备上下文关联的，当 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 查询设备上下文以获取屏幕分辨率时，不管实际屏幕分辨率是多少，结果通常都是 96。  通过在 <xref:System.Drawing.Graphics.DrawImage%2A> 方法中指定目标矩形，可以避免自动缩放图像。  
  
## 示例  
 下面的示例将相同的图像绘制两次。  在第一个例子中，未指定目标矩形的宽度和高度，图像被自动缩放。  在第二个例子中，目标矩形的宽度和高度（单位是像素）被指定为与原始图像的宽度和高度相同。  下面的插图显示两次呈现的图像。  
  
 ![经缩放的纹理](../../../../docs/framework/winforms/advanced/media/csscaledtexture1.png "csscaledtexture1")  
  
 [!code-csharp[System.Drawing.WorkingWithImages#32](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.WorkingWithImages#32](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#32)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  用系统上有效的图像名和路径替换 Texture.jpg。  
  
## 请参阅  
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [使用图像、位图、图标和图元文件](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)