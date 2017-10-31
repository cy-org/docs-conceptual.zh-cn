---
title: "如何：使用 Image 元素 | Microsoft Docs"
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
  - "BitmapImage 类"
  - "类, BitmapImage"
  - "控件, Image"
  - "Image 控件"
  - "呈现图像"
ms.assetid: 5b92e74b-1b56-4756-ac64-d5e9e08d9854
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：使用 Image 元素
本示例演示如何使用 <xref:System.Windows.Controls.Image> 元素在应用程序中包括图像。  
  
## 示例  
 下面的示例演示如何呈现 200 像素宽的图像。  在此[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 示例中，同时使用了特性语法和属性标记语法来定义图像。  有关特性语法或属性语法的更多信息，请参见[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  <xref:System.Windows.Media.Imaging.BitmapImage> 用于定义图像的源数据，并且是为属性标记语法示例显式定义的。  另外，<xref:System.Windows.Media.Imaging.BitmapImage> 的 <xref:System.Windows.Media.Imaging.BitmapImage.DecodePixelWidth%2A> 设置为与 <xref:System.Windows.Controls.Image> 的 <xref:System.Windows.FrameworkElement.Width%2A> 相同的宽度。  这是为了确保呈现图像使用的内存量最小。  
  
> [!NOTE]
>  通常，如果您希望指定所呈现图像的大小，请要么指定 <xref:System.Windows.FrameworkElement.Width%2A>，要么指定 <xref:System.Windows.FrameworkElement.Height%2A>，而不要两者都指定。  如果您仅指定其中之一，则会保持图像的[纵横比](GTMT)。  否则，图像可能会出现意外的拉伸或扭曲。  若要控制图像的拉伸行为，请使用 <xref:System.Windows.Controls.Image.Stretch%2A> 和 <xref:System.Windows.Controls.Image.StretchDirection%2A> 属性。  
  
> [!NOTE]
>  当通过 <xref:System.Windows.FrameworkElement.Width%2A> 或 <xref:System.Windows.FrameworkElement.Height%2A> 来指定图像的大小时，您还应分别将 <xref:System.Windows.Media.Imaging.BitmapImage.DecodePixelWidth%2A> 或 <xref:System.Windows.Media.Imaging.BitmapImage.DecodePixelHeight%2A> 设置为同样的大小。  
  
 <xref:System.Windows.Controls.Image.Stretch%2A> 属性确定如何拉伸图像源来填充图像元素。  有关更多信息，请参见 <xref:System.Windows.Media.Stretch>。  
  
 [!code-xml[ImageElementExample_snip#ImageSimpleExampleInlineMarkup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml#imagesimpleexampleinlinemarkup)]  
  
## 示例  
 下面的示例演示如何使用代码呈现 200 像素宽的图像。  
  
> [!NOTE]
>  必须在 <xref:System.Windows.Media.Imaging.BitmapImage.BeginInit%2A> 和 <xref:System.Windows.Media.Imaging.BitmapImage.EndInit%2A> 块内执行 <xref:System.Windows.Media.Imaging.BitmapImage> 属性的设置。  
  
 [!code-csharp[ImageElementExample_snip#ImageSimpleExampleInlineCode1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml.cs#imagesimpleexampleinlinecode1)]
 [!code-vb[ImageElementExample_snip#ImageSimpleExampleInlineCode1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/ImageSimpleExample.xaml.vb#imagesimpleexampleinlinecode1)]  
  
## 请参阅  
 [图像处理概述](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)