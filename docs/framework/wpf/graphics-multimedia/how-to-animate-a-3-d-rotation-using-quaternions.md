---
title: "如何：使用四元数对三维旋转进行动画处理 | Microsoft Docs"
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
  - "三维转换, 动画处理, 使用四元数"
  - "动画, 三维转换, 使用四元数"
  - "四元数"
ms.assetid: adca9cb1-066b-4de8-abbb-6b4007579ee7
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：使用四元数对三维旋转进行动画处理
本示例演示如何使用四元数对三维对象的旋转进行动画处理。  
  
 下面的代码显示了用作 <xref:System.Windows.Media.Media3D.RotateTransform3D> 的 <xref:System.Windows.Media.Media3D.RotateTransform3D.Rotation%2A> 属性值的 <xref:System.Windows.Media.Media3D.QuaternionRotation3D>。  
  
 [!code-xml[Animation3DGallery_snip#QuaternionAnimationExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationExample.xaml#quaternionanimationexampleinline1)]  
  
 下面的代码使用 <xref:System.Windows.Media.Animation.Storyboard> 内的 <xref:System.Windows.Media.Animation.QuaternionAnimation> 对此 <xref:System.Windows.Media.Media3D.QuaternionRotation3D> 进行动画处理。  
  
 [!code-xml[Animation3DGallery_snip#QuaternionAnimationExampleInline2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationExample.xaml#quaternionanimationexampleinline2)]  
  
## 示例  
 下面的代码显示了完整的示例。  
  
 [!code-xml[Animation3DGallery_snip#QuaternionAnimationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationExample.xaml#quaternionanimationexamplewholepage)]  
  
## 请参阅  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [创建三维场景](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-3-d-scene.md)   
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)   
 [变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [使用演示图板对三维旋转进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-storyboards.md)   
 [使用 Rotation3DAnimation 对三维旋转进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-rotation3danimation.md)