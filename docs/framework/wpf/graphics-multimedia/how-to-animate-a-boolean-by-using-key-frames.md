---
title: "如何：使用关键帧对布尔属性值进行动画处理 | Microsoft Docs"
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
  - "动画, 使用关键帧对布尔型属性值进行动画处理"
  - "布尔型, 使用关键帧进行动画处理"
  - "关键帧, 对布尔型属性值进行动画处理"
ms.assetid: 4b0fac96-6231-4fcf-9775-4dd673ddc785
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用关键帧对布尔属性值进行动画处理
本示例演示如何使用关键帧对 <xref:System.Windows.Controls.Button> 控件的布尔属性值进行动画处理。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.Animation.BooleanAnimationUsingKeyFrames> 类对 <xref:System.Windows.Controls.Button> 控件的 <xref:System.Windows.UIElement.IsEnabled%2A> 属性进行动画处理。  此示例中的所有关键帧都使用 <xref:System.Windows.Media.Animation.DiscreteBooleanKeyFrame> 类的一个实例。  诸如 <xref:System.Windows.Media.Animation.DiscreteBooleanKeyFrame> 的离散关键帧将创建突然跳跃值，也就是说，动画的移动是急拉动作。  
  
 [!code-csharp[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/BooleanAnimationUsingKeyFramesExample.cs#booleananimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/booleananimationusingkeyframesexample.vb#booleananimationusingkeyframeswholepage)]
 [!code-xml[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/BooleanAnimationUsingKeyFramesExample.xaml#booleananimationusingkeyframeswholepage)]  
  
 有关完整示例，请参见 [KeyFrame Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160012)（KeyFrame 动画示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.BooleanAnimationUsingKeyFrames>   
 <xref:System.Windows.UIElement.IsEnabled%2A>   
 <xref:System.Windows.Controls.Button>   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [关键帧动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)