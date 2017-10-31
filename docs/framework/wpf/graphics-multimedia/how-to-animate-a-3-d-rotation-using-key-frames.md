---
title: "如何：使用关键帧对三维旋转进行动画处理 | Microsoft Docs"
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
  - "三维转换, 动画处理, 使用关键帧 (Rotation3DAnimation)"
  - "动画, 三维转换, 使用关键帧 (Rotation3DAnimation)"
  - "关键帧, Rotation3DAnimation"
ms.assetid: 6f671b95-7f30-4836-9a4f-aeb7dc30121f
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用关键帧对三维旋转进行动画处理
在下面的示例中，在对三维对象的旋转轴进行动画处理时产生“摇摆不定”的情况下，<xref:System.Windows.Media.Animation.Rotation3DAnimationUsingKeyFrames> 用于对三维对象进行旋转。  此动画使用以下关键帧：  
  
1.  <xref:System.Windows.Media.Animation.LinearRotation3DKeyFrame> 用于创建值之间的平滑、线性内插。  
  
2.  <xref:System.Windows.Media.Animation.DiscreteRotation3DKeyFrame> 用于创建值之间的突然“跳转”（无内插）。  
  
3.  <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame> 用于根据 <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame.KeySpline%2A> 属性创建值之间的可变过渡。  在下面的示例中，此动画部分开始时速度很慢，之后速度按指数级增长，直至时间段结束。  
  
## 示例  
 [!code-xml[Animation3DGallery_snip#Rotation3DAnimationUsingKeyFramesExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Rotation3DAnimationUsingKeyFramesExample.xaml#rotation3danimationusingkeyframesexamplewholepage)]  
  
## 请参阅  
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [使用演示图板对三维旋转进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-storyboards.md)   
 [使用 Rotation3DAnimation 对三维旋转进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-rotation3danimation.md)   
 [使用四元数对三维旋转进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-quaternions.md)   
 [使用关键帧对三维旋转进行动画处理 \(QuaternionAnimationUsingKeyFrames\)](../../../../docs/framework/wpf/graphics-multimedia/animate-a-3-d-rotation-quaternionanimationusingkeyframes.md)