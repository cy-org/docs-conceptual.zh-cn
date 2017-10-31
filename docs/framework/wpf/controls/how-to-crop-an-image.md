---
title: "如何：裁剪图像 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "类, CroppedBitmap"
  - "CroppedBitmap 类"
  - "裁剪图像"
  - "图像, 裁剪"
ms.assetid: c6bba109-c6e7-4cf8-bfe6-9cf8d01bb4fc
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：裁剪图像
本示例演示如何使用 <xref:System.Windows.Media.Imaging.CroppedBitmap> 裁剪图像。  
  
 <xref:System.Windows.Media.Imaging.CroppedBitmap> 主要在对图像的裁剪版本进行编码以保存到文件时使用。  若要出于显示目的而裁剪图像，请参见[Create a Clip Region](http://msdn.microsoft.com/zh-cn/56e4bed6-78d7-4292-b917-d72d0b3e4376)主题。  
  
## 示例  
 下面的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 定义在下面的示例中使用的资源。  
  
 [!code-xml[imageelementexample#CroppedXAML1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml1)]  
  
 下面的示例使用 <xref:System.Windows.Media.Imaging.CroppedBitmap> 作为源来创建图像。  
  
 [!code-xml[imageelementexample#CroppedXAML2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml2)]  
  
 [!code-csharp[imageelementexample#CroppedCSharp1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml.cs#croppedcsharp1)]
 [!code-vb[imageelementexample#CroppedCSharp1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/CroppedImageExample.xaml.vb#croppedcsharp1)]  
  
 <xref:System.Windows.Media.Imaging.CroppedBitmap> 还可以用作另一个 <xref:System.Windows.Media.Imaging.CroppedBitmap> 的源，从而链接裁剪内容。  请注意，<xref:System.Windows.Media.Imaging.CroppedBitmap.SourceRect%2A> 使用相对于源裁剪位图的值，而不是使用相对于初始图像的值。  
  
 [!code-xml[imageelementexample#CroppedXAML3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml3)]  
  
 [!code-csharp[imageelementexample#CroppedCSharp2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml.cs#croppedcsharp2)]
 [!code-vb[imageelementexample#CroppedCSharp2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/CroppedImageExample.xaml.vb#croppedcsharp2)]  
  
## 请参阅  
 [Create a Clip Region](http://msdn.microsoft.com/zh-cn/56e4bed6-78d7-4292-b917-d72d0b3e4376)