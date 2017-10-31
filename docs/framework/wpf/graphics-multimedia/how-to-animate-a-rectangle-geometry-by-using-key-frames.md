---
title: "如何：使用关键帧对矩形几何形状进行动画处理 | Microsoft Docs"
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
  - "动画, 使用关键帧对 RectangleGeometry 对象进行动画处理"
  - "关键帧, 对 RectangleGeometry 对象进行动画处理"
  - "RectangleGeometry 对象, 使用关键帧进行动画处理"
ms.assetid: a8b45ceb-0e32-4ba1-928f-df6d30db17c6
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用关键帧对矩形几何形状进行动画处理
此示例演示如何使用关键帧对 <xref:System.Windows.Media.RectangleGeometry> 的 <xref:System.Windows.Media.RectangleGeometry.Rect%2A> 属性进行动画处理。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.Animation.RectAnimationUsingKeyFrames> 类对 <xref:System.Windows.Media.RectangleGeometry> 的 <xref:System.Windows.Media.RectangleGeometry.Rect%2A> 属性进行动画处理。  此动画按下列方式使用三个关键帧：  
  
1.  在前两秒中，使用 <xref:System.Windows.Media.Animation.LinearRectKeyFrame> 类的实例对矩形位置、宽度和高度的逐渐变化进行动画处理。  诸如 <xref:System.Windows.Media.Animation.LinearRectKeyFrame> 的线性关键帧在值之间创建平滑的线性过渡。  
  
2.  在接下来的半秒结束时，使用 <xref:System.Windows.Media.Animation.DiscreteRectKeyFrame> 类的实例突然减小矩形的高度。  离散关键帧（如 <xref:System.Windows.Media.Animation.DiscreteRectKeyFrame>）将使值发生突变，也就是说，高度减小是快速发生的，并且不是细微变化。  
  
3.  在最后两秒内，使用 <xref:System.Windows.Media.Animation.SplineRectKeyFrame> 类的实例将矩形更改回其原始大小和位置。  [样条](GTMT)关键帧（如 <xref:System.Windows.Media.Animation.SplineRectKeyFrame>）将会根据 <xref:System.Windows.Media.Animation.SplineRectKeyFrame.KeySpline%2A> 属性的值在各个值之间创建可变过渡。  在本例中，变化开始时比较缓慢，然后呈指数方式加速直到时间段结束。  
  
 [!code-csharp[keyframes_snip#RectAnimationUsingKeyFramesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/RectAnimationUsingKeyFramesExample.cs#rectanimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#RectAnimationUsingKeyFramesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/rectanimationusingkeyframesexample.vb#rectanimationusingkeyframeswholepage)]
 [!code-xml[keyframes_snip#RectAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/RectAnimationUsingKeyFramesExample.xaml#rectanimationusingkeyframeswholepage)]  
  
 有关完整示例，请参见 [KeyFrame Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160012)（KeyFrame 动画示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.RectangleGeometry>   
 <xref:System.Windows.Media.RectangleGeometry.Rect%2A>   
 <xref:System.Windows.Media.Animation.RectAnimationUsingKeyFrames>   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [关键帧动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)