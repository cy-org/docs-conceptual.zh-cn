---
title: "如何：使用 AnimationClock 对属性进行动画处理 | Microsoft Docs"
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
  - "动画, 属性, 使用 AnimationClocks"
  - "AnimationClocks"
ms.assetid: e6542021-714c-4675-9567-04f1c7380834
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：使用 AnimationClock 对属性进行动画处理
本示例演示如何使用 <xref:System.Windows.Media.Animation.Clock> 对象对属性进行动画处理。  
  
 可通过以下三种方法对[依赖项属性](GTMT)进行动画处理：  
  
-   使用 <xref:System.Windows.Media.Animation.Storyboard> 创建一个 <xref:System.Windows.Media.Animation.AnimationTimeline> 并将它与该属性关联。  
  
-   使用该对象的 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 方法向目标属性应用单个 <xref:System.Windows.Media.Animation.AnimationTimeline>。  
  
-   从 <xref:System.Windows.Media.Animation.AnimationTimeline> 创建一个 <xref:System.Windows.Media.Animation.AnimationClock> 并将它应用于某个属性。  
  
 使用 <xref:System.Windows.Media.Animation.Storyboard> 对象和 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 方法，可以在不直接创建和分发时钟的情况下对属性进行动画处理（有关示例，请参见[使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)和[在不使用演示图板的情况下对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md)）；系统会自动为您创建和分发时钟。  
  
## 示例  
 下面的示例演示如何创建一个 <xref:System.Windows.Media.Animation.AnimationClock> 并将其应用到两个相似的属性。  
  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/AnimationClockExample.cs#graphicsmmcreateanimationclockwholeclass)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/animationclockexample.vb#graphicsmmcreateanimationclockwholeclass)]  
  
 有关演示在 <xref:System.Windows.Media.Animation.Clock> 启动之后如何以交互方式对它进行控制的示例，请参见[以交互方式控制时钟](../../../../docs/framework/wpf/graphics-multimedia/how-to-interactively-control-a-clock.md)。  
  
## 请参阅  
 [使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)   
 [在不使用演示图板的情况下对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md)   
 [属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)