---
title: "如何：向动画起始值添加动画输出值 | Microsoft Docs"
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
  - "动画"
  - "IsAdditive 属性"
ms.assetid: b89a82be-b03d-481e-a8d3-cc513d09ca00
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：向动画起始值添加动画输出值
此示例演示如何向动画起始值添加动画输出值。  
  
## 示例  
 <xref:System.Windows.Media.Animation.DoubleAnimation.IsAdditive%2A> 属性指定是否将动画的输出值添加到已进行动画处理的属性的起始值（基值）。  您可以将 <xref:System.Windows.Media.Animation.DoubleAnimation.IsAdditive%2A> 属性用于大多数基本动画和大多数关键帧动画。  有关更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)和[关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)。  
  
 下面的示例演示将 <xref:System.Windows.Media.Animation.DoubleAnimation.IsAdditive%2A?displayProperty=fullName> 属性用于 <xref:System.Windows.Media.Animation.DoubleAnimation> 以及将 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsAdditive%2A?displayProperty=fullName> 属性用于 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 的效果。  
  
 [!code-xml[timingbehaviors_snip#IsAdditiveWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/IsAdditiveExample.xaml#isadditivewholepage)]  
  
## 请参阅  
 [在重复循环过程中累积动画值](../../../../docs/framework/wpf/graphics-multimedia/how-to-accumulate-animation-values-during-repeat-cycles.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Animation and Timing](http://msdn.microsoft.com/zh-cn/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)