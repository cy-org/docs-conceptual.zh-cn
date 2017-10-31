---
title: "如何：使用关键帧对点进行动画处理 | Microsoft Docs"
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
  - "动画, 使用关键帧对点进行动画处理"
  - "关键帧, 对点进行动画处理"
  - "点, 使用关键帧进行动画处理"
ms.assetid: d2e2ef10-0773-4133-856e-d41c09f60ded
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用关键帧对点进行动画处理
本示例演示如何使用 <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames> 类对 <xref:System.Windows.Point> 进行动画处理。  
  
## 示例  
 下面的示例将沿着三角形路径移动椭圆。  该示例使用 <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames> 类对 <xref:System.Windows.Media.EllipseGeometry> 的 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 属性进行动画处理。  此动画按下列方式使用三个关键帧：  
  
1.  在前半秒中，使用 <xref:System.Windows.Media.Animation.LinearPointKeyFrame> 类的实例将椭圆沿一条路径按固定速率从其起始位置移动。  诸如 <xref:System.Windows.Media.Animation.LinearPointKeyFrame> 的线性关键帧将在值之间创建平滑的线性内插。  
  
2.  在接下来的半秒，使用 <xref:System.Windows.Media.Animation.DiscretePointKeyFrame> 类的实例突然将椭圆沿着路径移动到下一个位置。  诸如 <xref:System.Windows.Media.Animation.DiscretePointKeyFrame> 的离散关键帧将创建突然跳跃值。  
  
3.  在最后两秒内，使用 <xref:System.Windows.Media.Animation.SplinePointKeyFrame> 类的实例将椭圆移回其起始位置。  [样条](GTMT)关键帧（如 <xref:System.Windows.Media.Animation.SplinePointKeyFrame>）将会根据 <xref:System.Windows.Media.Animation.SplinePointKeyFrame.KeySpline%2A> 属性的值在各个值之间创建可变过渡。  在本例中，动画开始时比较缓慢，然后按指数方式加速，直到时间段结束。  
  
 [!code-csharp[keyframes_snip#PointAnimationUsingKeyFramesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/PointAnimationUsingKeyFramesExample.cs#pointanimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#PointAnimationUsingKeyFramesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/pointanimationusingkeyframesexample.vb#pointanimationusingkeyframeswholepage)]
 [!code-xml[keyframes_snip#PointAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/PointAnimationUsingKeyFramesExample.xaml#pointanimationusingkeyframeswholepage)]  
  
 有关完整示例，请参见 [KeyFrame Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160012)（KeyFrame 动画示例）。  
  
 为了与其他动画示例保持一致，此示例的代码版本使用 <xref:System.Windows.Media.Animation.Storyboard> 对象来应用 <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>。  但是，在代码中应用单个动画时，较为简便的操作是使用 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 方法而非使用 <xref:System.Windows.Media.Animation.Storyboard>。  有关示例，请参见[在不使用演示图板的情况下对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>   
 <xref:System.Windows.Media.EllipseGeometry.Center%2A?displayProperty=fullName>   
 <xref:System.Windows.Media.EllipseGeometry>   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [关键帧动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)