---
title: "如何：使用关键帧对三维旋转进行动画处理 (QuaternionAnimationUsingKeyFrames) | Microsoft Docs"
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
  - "三维转换, 动画处理, 使用关键帧 (QuaternionAnimationUsingKeyFrames)"
  - "动画, 三维转换, 使用关键帧 (QuaternionAnimationUsingKeyFrames)"
  - "关键帧, QuaternionAnimationUsingKeyFrames"
ms.assetid: 09e5707b-7523-4a08-9aa7-bb13cbedccdf
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：使用关键帧对三维旋转进行动画处理 (QuaternionAnimationUsingKeyFrames)
在下面的示例中，<xref:System.Windows.Media.Animation.QuaternionAnimationUsingKeyFrames> 用于使一个三维对象旋转。  此动画使用以下关键帧：  
  
1.  <xref:System.Windows.Media.Animation.LinearRotation3DKeyFrame> 用于创建值之间的平滑、线性内插。  
  
2.  <xref:System.Windows.Media.Animation.DiscreteRotation3DKeyFrame> 用于创建值之间的突然“跳转”（无内插）。  
  
3.  <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame> 用于根据 <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame.KeySpline%2A> 属性创建值之间的可变过渡。  在下面的示例中，此动画部分开始时速度很慢，之后速度按指数级增长，直至时间段结束。  
  
## 示例  
 [!code-xml[Animation3DGallery_snip#QuaternionAnimationUsingKeyFramesExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationUsingKeyFramesExample.xaml#quaternionanimationusingkeyframesexamplewholepage)]  
  
## 请参阅  
 [使用演示图板对三维旋转进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-storyboards.md)   
 [使用 Rotation3DAnimation 对三维旋转进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-rotation3danimation.md)   
 [使用四元数对三维旋转进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-quaternions.md)   
 [使用关键帧对三维旋转进行动画处理 \(Rotation3DAnimationUsingKeyFrames\)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-key-frames.md)   
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)