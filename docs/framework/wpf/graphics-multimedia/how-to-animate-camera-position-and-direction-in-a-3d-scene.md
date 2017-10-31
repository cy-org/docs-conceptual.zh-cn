---
title: "如何：在三维场景中对照相机位置和方向进行动画处理 | Microsoft Docs"
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
  - "三维场景, 对照相机方向进行动画处理"
  - "三维场景, 对照相机位置进行动画处理"
  - "动画, 三维场景中的照相机方向"
  - "动画, 三维场景中的照相机位置"
  - "照相机方向, 在三维场景中进行动画处理"
  - "照相机位置, 在三维场景中进行动画处理"
ms.assetid: 480224b7-a5e5-4165-ba7f-ef760ddff94a
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：在三维场景中对照相机位置和方向进行动画处理
下面的示例演示如何在三维场景中对照相机的位置及其指向的方向进行动画处理。  执行此操作的方法是：使用 <xref:System.Windows.Media.Animation.Point3DAnimation> 和 <xref:System.Windows.Media.Animation.Vector3DAnimation> 分别对 <xref:System.Windows.Media.Media3D.PerspectiveCamera> 的 <xref:System.Windows.Media.Media3D.ProjectionCamera.Position%2A> 和 <xref:System.Windows.Media.Media3D.ProjectionCamera.LookDirection%2A> 属性进行动画处理。  您可以使用此种动画来更改响应某事件的、旁观者的场景视图。  
  
## 示例  
 [!code-xml[Animation3DGallery_snip#PointVector3DAnimationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/PointVector3DAnimationExample.xaml#pointvector3danimationexamplewholepage)]  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.Vector3DAnimation>   
 <xref:System.Windows.Media.Animation.Point3DAnimation>   
 [使用关键帧对照相机位置和方向进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-camera-position-and-direction-using-key-frames.md)   
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)