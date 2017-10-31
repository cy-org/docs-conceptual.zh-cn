---
title: "如何：缩放时使用插值模式控制图像质量 | Microsoft Docs"
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
  - "图像 [Windows 窗体], 控制质量"
  - "图像 [Windows 窗体], 缩放"
  - "插值模式, 控制图像质量"
ms.assetid: fde9bccf-8aa5-4b0d-ba4b-788740627b02
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：缩放时使用插值模式控制图像质量
<xref:System.Drawing.Graphics> 对象的插值模式会影响 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 缩放（拉伸和收缩）图像的方式。  <xref:System.Drawing.Drawing2D.InterpolationMode> 枚举定义了几种插值模式，其中一些模式显示在下面的列表中：  
  
-   <xref:System.Drawing.Drawing2D.InterpolationMode>  
  
-   <xref:System.Drawing.Drawing2D.InterpolationMode>  
  
-   <xref:System.Drawing.Drawing2D.InterpolationMode>  
  
-   <xref:System.Drawing.Drawing2D.InterpolationMode>  
  
-   <xref:System.Drawing.Drawing2D.InterpolationMode>  
  
 若要拉伸图像，原始图像中的每个像素都必须映射为较大图像中的一组像素。  若要收缩图像，必须将原始图像中成组的像素映射为较小图像中单个的像素。  执行这些映射的算法的效果决定缩放后图像的质量。  生成优质缩放图像的算法往往需要更长的处理时间。  在上面的列表中，<xref:System.Drawing.Drawing2D.InterpolationMode> 是质量最差的模式，<xref:System.Drawing.Drawing2D.InterpolationMode> 是质量最好的模式。  
  
 若要设置插值模式，请将 <xref:System.Drawing.Drawing2D.InterpolationMode> 枚举的一个成员分配给 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.InterpolationMode%2A> 属性。  
  
## 示例  
 下面的示例绘制一个图像，然后用三种不同的插值模式收缩图像。  
  
 下面的插图显示原始图像和三个较小的图像。  
  
 ![具有各种内插设置的图像](../../../../docs/framework/winforms/advanced/media/csgrapes1.png "csgrapes1")  
  
 [!code-csharp[System.Drawing.WorkingWithImages#81](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#81)]
 [!code-vb[System.Drawing.WorkingWithImages#81](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#81)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [使用图像、位图、图标和图元文件](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)