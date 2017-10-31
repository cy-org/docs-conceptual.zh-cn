---
title: "如何：使用关键帧对照相机位置和方向进行动画处理 | Microsoft Docs"
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
  - "动画, 使用关键帧对照相机方向进行动画处理"
  - "动画, 使用关键帧对照相机位置进行动画处理"
  - "照相机方向, 使用关键帧进行动画处理"
  - "照相机位置, 使用关键帧进行动画处理"
  - "关键帧, 对照相机方向进行动画处理"
  - "关键帧, 对照相机位置进行动画处理"
ms.assetid: 5753024e-0057-454d-947f-43ea686879c7
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：使用关键帧对照相机位置和方向进行动画处理
在下面的示例中，<xref:System.Windows.Media.Animation.Point3DAnimationUsingKeyFrames> 用于对三维场景中的 <xref:System.Windows.Media.Media3D.PerspectiveCamera> 位置进行动画处理。  此外，<xref:System.Windows.Media.Animation.Vector3DAnimationUsingKeyFrames> 用于在三维场景中对照相机指向的方向进行动画处理。  这两类动画都使用若干关键帧来创建一系列动画效果：  
  
1.  <xref:System.Windows.Media.Animation.LinearPoint3DKeyFrame> 和 <xref:System.Windows.Media.Animation.LinearVector3DKeyFrame> 用于创建值之间的平滑、线性内插。  
  
2.  <xref:System.Windows.Media.Animation.DiscretePoint3DKeyFrame> 和 <xref:System.Windows.Media.Animation.DiscreteVector3DKeyFrame> 用于创建值之间的突然“跳转”（无内插）。  
  
3.  <xref:System.Windows.Media.Animation.SplinePoint3DKeyFrame> 和 <xref:System.Windows.Media.Animation.SplineVector3DKeyFrame> 用于根据 <xref:System.Windows.Media.Animation.SplinePoint3DKeyFrame.KeySpline%2A> 属性创建值之间的可变过渡。  在下面的示例中，动画一开始较慢，但是随后以指数级加速，直至时间段结束。  
  
## 示例  
 [!code-xml[Animation3DGallery_snip#PointVector3DAnimationUsingKeyFramesExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/PointVector3DAnimationUsingKeyFramesExample.xaml#pointvector3danimationusingkeyframesexamplewholepage)]  
  
## 请参阅  
 [在三维场景中对照相机位置和方向进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-camera-position-and-direction-in-a-3d-scene.md)   
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)