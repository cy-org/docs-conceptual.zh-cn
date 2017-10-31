---
title: "如何：使用演示图板对三维旋转进行动画处理 | Microsoft Docs"
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
  - "三维转换, 动画处理, 使用演示图板"
  - "动画, 三维转换, 使用演示图板"
  - "情节提要"
ms.assetid: 1020e44e-e21e-49a8-be53-53cbc1910e83
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用演示图板对三维旋转进行动画处理
下面的示例演示如何在三维对象“摇摆不定”时对其进行旋转，具体方法是对 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D> 对象的 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Angle%2A> 和 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Axis%2A> 属性进行动画处理。  此 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D> 对象指定了三维对象的旋转变换，因此可对其属性进行动画处理，从而创建所需的旋转效果。  演示图板内的 <xref:System.Windows.Media.Animation.DoubleAnimation> 用于对 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Angle%2A> 属性进行动画处理，而 <xref:System.Windows.Media.Animation.Vector3DAnimation> 则用于对 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Axis%2A> 属性进行动画处理。  
  
## 示例  
 [!code-xml[Animation3DGallery_snip#Rotate3DUsingAxisAngleRotation3DExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Rotat3DUsingAxisAngleRotation3DExample.xaml#rotate3dusingaxisanglerotation3dexamplewholepage)]  
  
## 请参阅  
 [使用 Rotation3DAnimation 对三维旋转进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-rotation3danimation.md)   
 [使用关键帧对三维旋转进行动画处理 \(Rotation3DAnimationUsingKeyFrames\)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-key-frames.md)   
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)   
 [演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)