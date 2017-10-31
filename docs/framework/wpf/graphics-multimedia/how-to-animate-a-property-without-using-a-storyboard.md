---
title: "如何：在不使用演示图板的情况下对属性进行动画处理 | Microsoft Docs"
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
  - "动画, 非演示图板（本地）"
  - "本地动画"
  - "非演示图板动画"
ms.assetid: d411db70-4df7-487d-82bc-95a7c1b2e7f8
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：在不使用演示图板的情况下对属性进行动画处理
此示例演示了一种在不使用 <xref:System.Windows.Media.Animation.Storyboard> 的情况下对属性进行动画处理的方法。  
  
> [!NOTE]
>  在 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中无法使用此功能。  有关在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中对属性进行动画处理的信息，请参见[使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)。  
  
 若要对属性应用本地动画，请使用 <xref:System.Windows.UIElement.BeginAnimation%2A> 方法。  此方法将使用两个参数：用于指定要进行动画处理的属性和要应用于该属性的动画的 <xref:System.Windows.DependencyProperty>。  
  
## 示例  
 下面的示例演示如何对 <xref:System.Windows.Controls.Button> 的宽度和背景颜色进行动画处理。  
  
 [!code-cpp[animateproperty#11](../../../../samples/snippets/cpp/VS_Snippets_Wpf/animateproperty/CPP/LocalAnimationExample.cpp#11)]
 [!code-csharp[animateproperty#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animateproperty/CSharp/LocalAnimationExample.cs#11)]
 [!code-vb[animateproperty#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animateproperty/VisualBasic/LocalAnimationExample.vb#11)]  
  
 在 <xref:System.Windows.Media.Animation> 命名空间中，存在对不同类型的属性进行动画处理的各种动画类。  有关对属性进行动画处理的更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  有关[依赖项属性](GTMT)（在这些示例中显示的属性的类型）及其功能的更多信息，请参见[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  
  
 还有其他一些方法也可以在不使用 <xref:System.Windows.Media.Animation.Storyboard> 对象的情况下进行动画处理，有关更多信息，请参见[属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.AnimationTimeline>   
 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>   
 <xref:System.Windows.Media.Animation>   
 <xref:System.Windows.Media.Animation.Storyboard>   
 [属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)