---
title: "如何：确定编码器支持的参数 | Microsoft Docs"
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
  - "编码器参数, 确定支持的"
ms.assetid: f47ae459-e3ce-4d41-a140-2f6c6aea3f44
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：确定编码器支持的参数
可以调整图像参数，例如质量和压缩级别，但必须知道给定的图像编码器支持哪些参数。  <xref:System.Drawing.Image> 类提供了 <xref:System.Drawing.Image.GetEncoderParameterList%2A> 方法，以便您可以确定特定编码器支持哪些图像参数。  可使用 GUID 指定编码器。  <xref:System.Drawing.Image.GetEncoderParameterList%2A> 方法返回 <xref:System.Drawing.Imaging.EncoderParameter> 对象的数组。  
  
## 示例  
 下面的代码示例输出 JPEG 编码器支持的参数。  使用 <xref:System.Drawing.Imaging.Encoder> 类概述中的参数类别和关联的 GUID 列表，可确定每个参数的类别。  
  
 [!code-csharp[UsingImageEncodersDecoders#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#3)]
 [!code-vb[UsingImageEncodersDecoders#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#3)]  
  
## 编译代码  
 此示例需要：  
  
-   Windows 窗体应用程序。  
  
-   <xref:System.Windows.Forms.PaintEventArgs>，它是 <xref:System.Windows.Forms.PaintEventHandler> 的一个参数。  
  
## 请参阅  
 [如何：列出已安装的解码器](../../../../docs/framework/winforms/advanced/how-to-list-installed-encoders.md)   
 [位图类型](../../../../docs/framework/winforms/advanced/types-of-bitmaps.md)   
 [在托管 GDI\+ 中使用图像编码器和解码器](../../../../docs/framework/winforms/advanced/using-image-encoders-and-decoders-in-managed-gdi.md)