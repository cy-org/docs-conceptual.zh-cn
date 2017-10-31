---
title: "如何：将 BMP 图像转换为 PNG 图像 | Microsoft Docs"
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
  - "BMP 图像, 转换为 PNG"
  - "图像格式, 转换"
ms.assetid: 9d4a692d-73ac-4ce3-9e05-9ec321e8fbd6
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：将 BMP 图像转换为 PNG 图像
通常，需要转换图像文件格式。  可以通过调用 <xref:System.Drawing.Image> 类的 <xref:System.Drawing.Image.Save%2A> 方法，并将 <xref:System.Drawing.Imaging.ImageFormat> 指定为所需的图像文件格式来轻松完成转换。  
  
## 示例  
 以下示例从一个类型加载 BMP 图像，并以 PNG 格式保存该图像。  
  
 [!code-csharp[UsingImageEncodersDecoders#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#4)]
 [!code-vb[UsingImageEncodersDecoders#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#4)]  
  
## 编译代码  
 此示例需要：  
  
-   Windows 窗体应用程序。  
  
-   对 `System.Drawing.Imaging` 命名空间的引用。  
  
## 请参阅  
 [如何：列出已安装的解码器](../../../../docs/framework/winforms/advanced/how-to-list-installed-encoders.md)   
 [在托管 GDI\+ 中使用图像编码器和解码器](../../../../docs/framework/winforms/advanced/using-image-encoders-and-decoders-in-managed-gdi.md)   
 [位图类型](../../../../docs/framework/winforms/advanced/types-of-bitmaps.md)