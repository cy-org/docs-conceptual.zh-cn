---
title: "如何：使用关键帧对双精度属性值进行动画处理 | Microsoft Docs"
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
  - "动画, 使用关键帧对双精度属性值进行动画处理"
  - "双精度值, 使用关键帧进行动画处理"
  - "关键帧, 对双精度属性值进行动画处理"
ms.assetid: 3a1a7dba-7694-4907-8a2f-3408baebfa82
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：使用关键帧对双精度属性值进行动画处理
此示例演示如何使用关键帧对采用 <xref:System.Double> 的属性的值进行动画处理。  
  
## 示例  
 下面的示例将一个矩形从屏幕一端移到另一端。  此示例使用 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 类对应用于 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Media.TranslateTransform> 的 <xref:System.Windows.Media.TranslateTransform.X%2A> 属性进行动画处理。  此动画（无限期地重复）按下列方式使用三个关键帧：  
  
1.  在最初三秒内，将使用 <xref:System.Windows.Media.Animation.LinearDoubleKeyFrame> 类的实例，使该矩形沿着某个路径以固定的速率从其起始位置移到 500 位置。  线性关键帧（如 <xref:System.Windows.Media.Animation.LinearDoubleKeyFrame>）将在值之间创建平滑的线性过渡。  
  
2.  在第四秒结束时，将使用 <xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame> 类的实例，使矩形在一瞬间移到下一个位置。  离散关键帧（如 <xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame>）将在值之间创建突然跳转。  在本例中，矩形位于起始位置，然后突然出现在 500 位置。  
  
3.  在最后两秒钟内，使用 <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame> 类的实例将矩形移回其起始位置。  [样条](GTMT)关键帧（如 <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame>）将会根据 <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame.KeySpline%2A> 属性的值在各个值之间创建可变过渡。  在本例中，矩形开始时缓慢移动，然后其速度以指数级加快，直到时间段结束。  
  
 [!code-csharp[keyframes_snip#AltDoubleAnimationUsingKeyFramesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/AltDoubleAnimationUsingKeyFramesExample.cs#altdoubleanimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#AltDoubleAnimationUsingKeyFramesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/altdoubleanimationusingkeyframesexample.vb#altdoubleanimationusingkeyframeswholepage)]
 [!code-xml[keyframes_snip#AltDoubleAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/AltDoubleAnimationUsingKeyFramesExample.xaml#altdoubleanimationusingkeyframeswholepage)]  
  
 有关完整示例，请参见 [KeyFrame Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160012)（KeyFrame 动画示例）。  
  
 为了与其他动画示例保持一致，此示例的代码版本使用 <xref:System.Windows.Media.Animation.Storyboard> 对象来应用 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>。  此外，在代码中应用单个动画时，更简便的做法是使用 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 方法而不是 <xref:System.Windows.Media.Animation.Storyboard>。  有关示例，请参见[在不使用演示图板的情况下对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>   
 <xref:System.Windows.Shapes.Rectangle>   
 <xref:System.Windows.Media.Animation.LinearDoubleKeyFrame>   
 <xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame>   
 <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame>   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [关键帧动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)