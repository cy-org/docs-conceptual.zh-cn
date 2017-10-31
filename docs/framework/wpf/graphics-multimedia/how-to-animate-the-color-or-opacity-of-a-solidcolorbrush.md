---
title: "如何：对 SolidColorBrush 的颜色或不透明度进行动画处理 | Microsoft Docs"
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
  - "动画, SolidColorBrush 的颜色"
  - "动画, SolidColorBrush 的不透明度"
  - "颜色, 动画处理"
  - "不透明度, 动画处理"
  - "SolidColorBrush, 对颜色进行动画处理"
  - "SolidColorBrush, 对不透明度进行动画处理"
ms.assetid: d9154354-843f-4713-bad1-35bb0ba6eaeb
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：对 SolidColorBrush 的颜色或不透明度进行动画处理
本示例演示如何对 <xref:System.Windows.Media.SolidColorBrush> 的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 和 <xref:System.Windows.Media.Brush.Opacity%2A> 进行动画处理。  
  
## 示例  
 下面的示例使用三个动画对 <xref:System.Windows.Media.SolidColorBrush> 的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 和 <xref:System.Windows.Media.Brush.Opacity%2A> 进行动画处理。  
  
-   当鼠标进入矩形时，第一个动画（一个 <xref:System.Windows.Media.Animation.ColorAnimation>）会将画笔的颜色改为 <xref:System.Windows.Media.Colors.Gray%2A>。  
  
-   当鼠标离开矩形时，第二个动画（另一个 <xref:System.Windows.Media.Animation.ColorAnimation>）会将画笔的颜色改为 <xref:System.Windows.Media.Colors.Orange%2A>。  
  
-   在按下鼠标左键时，最后一个动画（一个 <xref:System.Windows.Media.Animation.DoubleAnimation>）会将画笔的不透明度改为 0.0。  
  
 [!code-csharp[brushanimations_snip#SolidColorBrushAnimationExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushanimations_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushanimationexample)]  
  
 有关演示如何对不同类型的画笔进行动画处理的更完整示例，请参见 [Brushes Sample](http://go.microsoft.com/fwlink/?LinkID=159973)（画笔示例）。  有关动画的更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
 为了与其他动画示例保持一致，此示例的代码版本使用 <xref:System.Windows.Media.Animation.Storyboard> 对象来应用它们的动画。  但是，在代码中应用单个动画时，较为简便的操作是使用 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 方法而非使用 <xref:System.Windows.Media.Animation.Storyboard>。  有关示例，请参见[在不使用演示图板的情况下对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md)。  
  
## 请参阅  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)   
 [Brushes Sample](http://go.microsoft.com/fwlink/?LinkID=159973)