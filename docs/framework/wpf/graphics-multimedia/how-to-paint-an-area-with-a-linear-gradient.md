---
title: "如何：绘制带有线性渐变的区域 | Microsoft Docs"
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
  - "画笔, 使用线性渐变进行绘制"
  - "线性渐变, 绘制"
  - "绘制, 使用线性渐变"
ms.assetid: 00e0cd04-48c0-4ec5-850e-d321beb37a34
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：绘制带有线性渐变的区域
本示例演示如何使用 <xref:System.Windows.Media.LinearGradientBrush> 类来绘制带有线性渐变的区域。  在下面的示例中，<xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Shapes.Shape.Fill%2A> 是用从黄色依次过渡到红色、蓝色和浅绿色的对角线性渐变来绘制的。  
  
## 示例  
 [!code-xml[GradientBrushExamples_snip#DiagonalGradient1XAML](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#diagonalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#DiagonalGradient1CSharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#diagonalgradient1csharp)]  
  
 下图显示了上一示例创建的渐变。  
  
 ![对角线方向线性渐变](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-diagonallgb.png "graphicsmm\_DiagonalLGB")  
  
 若要创建水平线性渐变，请将 <xref:System.Windows.Media.LinearGradientBrush> 的 <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> 和 <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> 分别改为 \(0,0.5\) 和 \(1,0.5\)。  在下面的示例中，<xref:System.Windows.Shapes.Rectangle> 是用水平线性渐变来绘制的。  
  
 [!code-xml[GradientBrushExamples_snip#HorizontalGradient1XAML](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#horizontalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#HorizontalGradient1CSharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#horizontalgradient1csharp)]  
  
 下图显示了上一示例创建的渐变。  
  
 ![水平线性渐变](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-horizontallgb.png "graphicsmm\_HorizontalLGB")  
  
 若要创建垂直线性渐变，请将 <xref:System.Windows.Media.LinearGradientBrush> 的 <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> 和 <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> 分别改为 \(0.5,0\) 和 \(0.5,1\)。  在下面的示例中，<xref:System.Windows.Shapes.Rectangle> 是用垂直线性渐变来绘制的。  
  
 [!code-xml[GradientBrushExamples_snip#VerticalGradient1XAML](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#verticalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#VerticalGradient1CSharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#verticalgradient1csharp)]  
  
 下图显示了上一示例创建的渐变。  
  
 ![垂直线性渐变](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-verticallgb.png "graphicsmm\_VerticalLGB")  
  
> [!NOTE]
>  此主题中的示例使用默认坐标系来设置起点和终点。  默认坐标系是相对于边界框的：0 表示边界框的 0%，1 表示边界框的 100%。  可以通过将 <xref:System.Windows.Media.GradientBrush.MappingMode%2A> 属性设置为值 <xref:System.Windows.Media.BrushMappingMode?displayProperty=fullName> 来更改此坐标系。  绝对坐标系与边界框不相关。  值直接在本地坐标系中解释。  
  
 有关其他示例，请参见 [Brushes Sample](http://go.microsoft.com/fwlink/?LinkID=159973)（画笔示例）。  有关渐变以及其他类型的画笔的更多信息，请参见[使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)。