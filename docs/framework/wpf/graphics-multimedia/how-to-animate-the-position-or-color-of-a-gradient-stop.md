---
title: "如何：对渐变停止点的位置或颜色进行动画处理 | Microsoft Docs"
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
  - "动画, GradientStop 对象的颜色"
  - "动画, GradientStop 对象的位置"
  - "颜色, 动画处理"
  - "GradientStop 对象, 对颜色进行动画处理"
  - "GradientStop 对象, 对位置进行动画处理"
  - "位置, 动画处理"
ms.assetid: 6f5b8b47-6c32-4b8e-98ee-fdf6515ec843
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：对渐变停止点的位置或颜色进行动画处理
本示例演示如何对 <xref:System.Windows.Media.GradientStop> 对象的 <xref:System.Windows.Media.GradientStop.Color%2A> 和 <xref:System.Windows.Media.GradientStop.Offset%2A> 进行动画处理。  
  
## 示例  
 下面的示例对 <xref:System.Windows.Media.LinearGradientBrush> 中的三个渐变停止点进行动画处理。  本示例使用三个动画，每个动画都对一个不同的渐变停止点进行动画处理：  
  
-   第一个动画（即 <xref:System.Windows.Media.Animation.DoubleAnimation>）对第一个渐变停止点的 <xref:System.Windows.Media.GradientStop.Offset%2A> 进行动画处理，使其从 0.0 到 1.0 然后回到 0.0。  因此，该渐变中的第一种颜色会从矩形的左侧移动到右侧，然后移动回到左侧。  
  
-   第二个动画（即 <xref:System.Windows.Media.Animation.ColorAnimation>）对第二个渐变停止点的 <xref:System.Windows.Media.GradientStop.Color%2A> 进行动画处理，使从 <xref:System.Windows.Media.Colors.Purple%2A> 变为 <xref:System.Windows.Media.Colors.Yellow%2A> 然后又变回 <xref:System.Windows.Media.Colors.Purple%2A>。  因此，该渐变中位于中间的颜色会从紫色改为黄色，之后又改回紫色。  
  
-   第三个动画（即另一个 <xref:System.Windows.Media.Animation.ColorAnimation>）以 \-1 为增量对第三个渐变停止点的 <xref:System.Windows.Media.GradientStop.Color%2A> 的不透明度进行动画处理，之后又进行相反的处理。  因此，该渐变中的第三种颜色会褪掉，之后再次变为不透明。  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/GradientStopAnimationExample.cs#graphicsmmgradientanimationexampleswholepage)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/gradientstopanimationexample.vb#graphicsmmgradientanimationexampleswholepage)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/GradientStopAnimationExample.xaml#graphicsmmgradientanimationexampleswholepage)]  
  
 尽管本示例使用 <xref:System.Windows.Media.LinearGradientBrush>，但是其过程与对 <xref:System.Windows.Media.RadialGradientBrush> 中的 <xref:System.Windows.Media.GradientStop> 对象进行动画处理相同。  
  
 有关其他示例，请参见 [Brushes Sample](http://go.microsoft.com/fwlink/?LinkID=159973)（画笔示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.GradientStop>   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)