---
title: "如何：设置 JPEG 压缩级别 | Microsoft Docs"
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
  - "图像 [Windows 窗体], 更改编码器参数"
  - "JPEG 图像, 设置质量级别"
ms.assetid: 4b9a74e3-9504-43c1-9f28-ace651d0772e
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：设置 JPEG 压缩级别
将图像保存到磁盘中时，可能需要修改图像的参数以最大限度地减小文件的大小或提高质量。  可以通过修改 JPEG 图像的压缩级别来调整其质量。  若要在保存 JPEG 图像时指定压缩级别，必须创建一个 <xref:System.Drawing.Imaging.EncoderParameters> 对象，并且将此对象传递给 <xref:System.Drawing.Image> 类的 <xref:System.Drawing.Image.Save%2A> 方法。  初始化 <xref:System.Drawing.Imaging.EncoderParameters> 对象，以使其具有包含一个 <xref:System.Drawing.Imaging.EncoderParameter> 的数组。  创建 <xref:System.Drawing.Imaging.EncoderParameter> 时，指定 <xref:System.Drawing.Imaging.Encoder.Quality> 编码器和所需的压缩级别。  
  
## 示例  
 下面的代码示例创建一个 <xref:System.Drawing.Imaging.EncoderParameter> 对象并保存三幅 JPEG 图像。  通过修改传递给 <xref:System.Drawing.Imaging.EncoderParameter> 构造函数的 `long` 值，使用不同的质量级别保存每个 JPEG 图像。  质量级别 0 对应于最大压缩，而质量级别 100 对应于最小压缩。  
  
 [!code-csharp[UsingImageEncodersDecoders#8](../../../../samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#8)]
 [!code-vb[UsingImageEncodersDecoders#8](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#8)]  
[!code-csharp[UsingImageEncodersDecoders#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#6)]
[!code-vb[UsingImageEncodersDecoders#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#6)]  
  
## 编译代码  
 此示例需要：  
  
-   Windows 窗体应用程序。  
  
-   <xref:System.Windows.Forms.PaintEventArgs>，它是 <xref:System.Windows.Forms.PaintEventHandler> 的一个参数。  
  
-   一个位于 **c:\\** 位置的名为 `TestPhoto.jpg` 的图像文件。  
  
## 请参阅  
 [如何：确定编码器支持的参数](../../../../docs/framework/winforms/advanced/how-to-determine-the-parameters-supported-by-an-encoder.md)   
 [位图类型](../../../../docs/framework/winforms/advanced/types-of-bitmaps.md)   
 [在托管 GDI\+ 中使用图像编码器和解码器](../../../../docs/framework/winforms/advanced/using-image-encoders-and-decoders-in-managed-gdi.md)