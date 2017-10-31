---
title: "如何：使用径向渐变绘制区域 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "画笔, 使用径向渐变进行绘制"
  - "绘制, 使用径向渐变"
  - "径向渐变, 绘制"
ms.assetid: b5d0fc8a-8986-4796-b003-a75b41a48928
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用径向渐变绘制区域
本示例演示如何使用 <xref:System.Windows.Media.RadialGradientBrush> 类来绘制带有径向渐变的区域。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.RadialGradientBrush> 来绘制一个具有径向渐变的矩形，此渐变从黄色依次过渡到红色、蓝色和浅绿色。  
  
 [!code-csharp[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/RadialGradientBrushSnippet.cs#simpleradialgradientexamplewholepage)]
 [!code-vb[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/radialgradientbrushsnippet.vb#simpleradialgradientexamplewholepage)]
 [!code-xml[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/RadialGradientBrushSnippet.xaml#simpleradialgradientexamplewholepage)]  
  
 下图显示了上述示例中的渐变。  其中突出显示了渐变的停止点。  
  
 ![径向渐变中的渐变停止点](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-4gradientstops-rg.png "wcpsdk\_graphicsmm\_4gradientstops\_rg")  
  
> [!NOTE]
>  本主题中的示例使用默认坐标系来设置控制点。  默认坐标系是相对于边界框的：0 表示边界框的 0%，1 表示边界框的 100%。  可以通过将 <xref:System.Windows.Media.GradientBrush.MappingMode%2A> 属性设置为值 <xref:System.Windows.Media.BrushMappingMode>，更改此坐标系。  绝对坐标系与边界框不相关。  值直接在本地坐标系中解释。  
  
 有关其他 <xref:System.Windows.Media.RadialGradientBrush> 示例，请参见 [Brushes Sample](http://go.microsoft.com/fwlink/?LinkID=159973)（画笔示例）。  有关渐变以及其他类型的画笔的更多信息，请参见[使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)。