---
title: "如何：使用关键帧对颜色进行动画处理 | Microsoft Docs"
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
  - "动画, 使用关键帧对颜色进行动画处理"
  - "颜色, 使用关键帧进行动画处理"
  - "关键帧, 对颜色进行动画处理"
ms.assetid: ab04ffa6-4de9-4d5b-a3b4-4e35d5b2ef35
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用关键帧对颜色进行动画处理
此示例演示如何使用关键帧对 <xref:System.Windows.Media.SolidColorBrush> 的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 进行动画处理。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames> 类对 <xref:System.Windows.Media.SolidColorBrush> 的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 属性进行动画处理。  此动画按下列方式使用三个关键帧：  
  
1.  在前两秒中，使用 <xref:System.Windows.Media.Animation.LinearColorKeyFrame> 类的实例逐渐将颜色从绿色变为红色。  诸如 <xref:System.Windows.Media.Animation.LinearColorKeyFrame> 的线性关键帧在值之间创建平滑的线性过渡。  
  
2.  在接下来的半秒结束时，使用 <xref:System.Windows.Media.Animation.DiscreteColorKeyFrame> 类的实例快速将颜色从红色变为黄色。  离散关键帧（如 <xref:System.Windows.Media.Animation.DiscreteColorKeyFrame>）将使值发生突变，也就是说，动画此部分中的颜色变化是快速发生的，并且不是细微变化。  
  
3.  在最后两秒内，使用 <xref:System.Windows.Media.Animation.SplineColorKeyFrame> 类的实例再次更改颜色 — 这一次从黄色变回绿色。  [样条](GTMT)关键帧（如 <xref:System.Windows.Media.Animation.SplineColorKeyFrame>）将会根据 <xref:System.Windows.Media.Animation.SplineColorKeyFrame.KeySpline%2A> 属性的值在各个值之间创建可变过渡。  在本例中，颜色变化开始时比较缓慢，然后呈指数方式加速直到时间段结束。  
  
 [!code-csharp[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/ColorAnimationUsingKeyFramesExample.cs#coloranimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/coloranimationusingkeyframesexample.vb#coloranimationusingkeyframeswholepage)]
 [!code-xml[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ColorAnimationUsingKeyFramesExample.xaml#coloranimationusingkeyframeswholepage)]  
  
 有关完整示例，请参见 [KeyFrame Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160012)（KeyFrame 动画示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.SolidColorBrush.Color%2A>   
 <xref:System.Windows.Media.SolidColorBrush>   
 <xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [关键帧动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)