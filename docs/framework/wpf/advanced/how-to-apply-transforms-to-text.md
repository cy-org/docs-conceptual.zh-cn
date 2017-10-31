---
title: "如何：向文本应用变换 | Microsoft Docs"
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
  - "旋转的文本"
  - "缩放的文本"
  - "隐藏的文本"
  - "扭曲的文本"
  - "文本变换"
  - "翻译的文本"
  - "版式, 旋转的文本"
  - "版式, 缩放的文本"
  - "版式, 隐藏的文本"
  - "版式, 扭曲的文本"
  - "版式, 转换"
  - "版式, 翻译的文本"
ms.assetid: 0d61678a-4185-4f2a-85c6-c1d020f96fa0
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：向文本应用变换
变换可以改变应用程序中文本的显示。  下面的示例使用不同类型的呈现变换来影响 <xref:System.Windows.Controls.TextBlock> 控件中文本的显示。  
  
## 示例  
 下面的示例演示围绕 x\-y 二维平面上的一个指定点旋转的文本。  
  
 ![使用 RotateTransform 旋转的文本](../../../../docs/framework/wpf/advanced/media/transformedtext01.png "TransformedText01")  
文本旋转 90 度的示例  
  
 下面的代码示例使用 <xref:System.Windows.Media.RotateTransform> 来旋转文本。  如果 <xref:System.Windows.Media.RotateTransform.Angle%2A> 值为 90，则按顺时针方向将元素旋转 90 度。  
  
 [!code-xml[TextTransformSample#TextTransformSample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTransformSample/CS/Window1.xaml#texttransformsample1)]  
  
 下面的示例演示三行文本，将第一行文本沿着 X 轴放大 150% 得到第二行文本，沿着 Y 轴放大 150% 得到第三行文本。  
  
 ![使用 ScaleTransform 缩放的文本](../../../../docs/framework/wpf/advanced/media/transformedtext02.png "TransformedText02")  
缩放的文本的示例  
  
 下面的代码示例使用 <xref:System.Windows.Media.ScaleTransform> 从文本原始大小对文本进行缩放。  
  
 [!code-xml[TextTransformSample#TextTransformSample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTransformSample/CS/Window1.xaml#texttransformsample2)]  
  
> [!NOTE]
>  放大文本与增大文本的字号不同。  字号的计算相互独立，以便提供针对不同字号的最佳分辨率。  另一方面，缩放后的文本将保持原始大小的文本的比例。  
  
 下面的示例演示沿 X 轴扭曲的文本。  
  
 ![使用 SkewTransform 扭曲的文本](../../../../docs/framework/wpf/advanced/media/transformedtext03.png "TransformedText03")  
扭曲的文本的示例  
  
 下面的代码示例使用 <xref:System.Windows.Media.SkewTransform> 来扭曲文本。  扭曲（也称为修剪）是一种以非均匀方式拉伸坐标空间的变换。  在本示例中，两个文本字符串沿 x 坐标扭曲了 \-30° 和 30°。  
  
 [!code-xml[TextTransformSample#TextTransformSample3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTransformSample/CS/Window1.xaml#texttransformsample3)]  
  
 下面的示例演示沿 x 轴和 y 轴平移或移动的文本。  
  
 ![使用 TranslateTransform 偏移的文本](../../../../docs/framework/wpf/advanced/media/transformedtext04.png "TransformedText04")  
平移的文本的示例  
  
 下面的代码示例使用 <xref:System.Windows.Media.TranslateTransform> 来偏移文本。  在本示例中，原始文本下方略微偏移的文本副本产生了阴影效果。  
  
 [!code-xml[TextTransformSample#TextTransformSample4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTransformSample/CS/Window1.xaml#texttransformsample4)]  
  
> [!NOTE]
>  <xref:System.Windows.Media.Effects.DropShadowBitmapEffect> 提供了一组丰富的功能来产生阴影效果。  有关更多信息，请参见[创建具有阴影的文本](../../../../docs/framework/wpf/advanced/how-to-create-text-with-a-shadow.md)。  
  
## 请参阅  
 [向文本应用动画](../../../../docs/framework/wpf/advanced/how-to-apply-animations-to-text.md)