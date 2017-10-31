---
title: "在托管 GDI+ 中使用图像编码器和解码器 | Microsoft Docs"
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
  - "图像解码器, using"
  - "图像编码器, using"
ms.assetid: 0e838ea1-4e7e-4334-b882-ab25df607b8b
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 在托管 GDI+ 中使用图像编码器和解码器
<xref:System.Drawing> 命名空间提供用于存储和操作图像的 <xref:System.Drawing.Image> 和 <xref:System.Drawing.Bitmap> 类。  通过在 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 中使用图像编码器，可以将图像从内存写入到磁盘中。通过在 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 中使用图像解码器，可以将图像从磁盘加载到内存中。  编码器将 <xref:System.Drawing.Image> 或 <xref:System.Drawing.Bitmap> 对象中的数据转换为指定的磁盘文件格式。  解码器将磁盘文件中的数据转换为 <xref:System.Drawing.Image> 和 <xref:System.Drawing.Bitmap> 对象所需要的格式。  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 具有支持以下文件类型的内置编码器和解码器：  
  
-   BMP  
  
-   GIF  
  
-   JPEG  
  
-   PNG  
  
-   TIFF  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 同样具有支持以下文件类型的内置解码器：  
  
-   WMF  
  
-   EMF  
  
-   图标  
  
 下列主题更详细地讨论了编码器和解码器：  
  
## 本节内容  
 [如何：列出已安装的解码器](../../../../docs/framework/winforms/advanced/how-to-list-installed-encoders.md)  
 描述如何列出计算机上的可用编码器。  
  
 [如何：列出已安装的解码器](../../../../docs/framework/winforms/advanced/how-to-list-installed-decoders.md)  
 描述如何列出计算机上的可用解码器。  
  
 [如何：确定编码器支持的参数](../../../../docs/framework/winforms/advanced/how-to-determine-the-parameters-supported-by-an-encoder.md)  
 描述如何列出编码器支持的 <xref:System.Drawing.Imaging.EncoderParameters>。  
  
 [如何：将 BMP 图像转换为 PNG 图像](../../../../docs/framework/winforms/advanced/how-to-convert-a-bmp-image-to-a-png-image.md)  
 描述如何以不同的图像格式保存图像。  
  
 [如何：设置 JPEG 压缩级别](../../../../docs/framework/winforms/advanced/how-to-set-jpeg-compression-level.md)  
 描述如何更改图像的质量级别。  
  
## 参考  
 <xref:System.Drawing.Image>  
  
 <xref:System.Drawing.Bitmap>  
  
 <xref:System.Drawing.Imaging.ImageCodecInfo>  
  
 <xref:System.Drawing.Imaging.EncoderParameter>  
  
 <xref:System.Drawing.Imaging.Encoder>  
  
## 相关章节  
 [关于 GDI\+ 托管代码](../../../../docs/framework/winforms/advanced/about-gdi-managed-code.md)  
  
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)