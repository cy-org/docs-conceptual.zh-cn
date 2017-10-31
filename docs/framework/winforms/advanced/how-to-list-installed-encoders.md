---
title: "如何：列出已安装的解码器 | Microsoft Docs"
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
  - "图像编解码器, 列出"
  - "图像编码器, 列出"
ms.assetid: 49e8e4e9-7a67-42d9-86bf-08821cdc282e
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：列出已安装的解码器
可能需要列出计算机上可用的图像编码器，以确定应用程序是否可以保存某种特定的图像文件格式。  <xref:System.Drawing.Imaging.ImageCodecInfo> 类提供了 <xref:System.Drawing.Imaging.ImageCodecInfo.GetImageEncoders%2A> 静态方法，以便您可以确定有哪些图像编码器可供使用。  <xref:System.Drawing.Imaging.ImageCodecInfo.GetImageEncoders%2A> 返回 <xref:System.Drawing.Imaging.ImageCodecInfo> 对象的数组。  
  
## 示例  
 下面的代码示例输出已安装的编码器及其属性值的列表。  
  
 [!code-csharp[UsingImageEncodersDecoders#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#1)]
 [!code-vb[UsingImageEncodersDecoders#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#1)]  
  
## 编译代码  
 此示例需要：  
  
-   Windows 窗体应用程序。  
  
-   <xref:System.Windows.Forms.PaintEventArgs>，它是 <xref:System.Windows.Forms.PaintEventHandler> 的一个参数。  
  
## 请参阅  
 [如何：列出已安装的解码器](../../../../docs/framework/winforms/advanced/how-to-list-installed-decoders.md)   
 [在托管 GDI\+ 中使用图像编码器和解码器](../../../../docs/framework/winforms/advanced/using-image-encoders-and-decoders-in-managed-gdi.md)