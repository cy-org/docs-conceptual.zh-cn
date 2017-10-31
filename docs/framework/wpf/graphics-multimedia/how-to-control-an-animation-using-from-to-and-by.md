---
title: "如何：使用 From、To 和 By 控制动画 | Microsoft Docs"
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
  - "动画、 从/到/by"
  - "基本动画"
  - "动画，基本动画"
  - "From/to/by 动画"
ms.assetid: 59afba57-6fc1-44c8-987e-8a5f4142adad
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用 From、To 和 By 控制动画
"From/To/By"或"基本动画"创建两个目标值之间的转换 (请参阅[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)有关不同类型的动画的介绍)。 若要设置基本动画目标值，使用其<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>，<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>，和<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性。  下表总结了如何<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>，<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>，和<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性可能会一起或单独来确定动画的目标值。  
  
|指定的属性|产生的行为|  
|--------------------------|------------------------|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>|动画从指定的值<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性设为正在进行动画处理的属性的基础价值或前一动画的输出值，具体取决于前一动画的配置方式。|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> and                              <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>|动画从指定的值<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性设置为指定的值<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性。|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> and                              <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>|动画从指定的值<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性设置为指定的总和的值<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>和<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性。|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>|该动画从动画的属性的基值的逐步过程或前一动画的输出到指定的值的值<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性。|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>|动画从正在进行动画处理的属性的基础价值或前一动画的输出到该值与指定的值之和的值<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性。|  
  
> [!NOTE]
>  请勿同时设置<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性和<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>上相同的动画的属性。  
  
 若要使用其他内插方法或对两个以上的目标值之间进行动画处理，请使用关键帧动画。 请参阅[关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)有关详细信息。  
  
 有关将多个动画应用于单个属性的信息，请参阅[关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)。  
  
 下面的示例演示设置了不同效果<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>，<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>，和<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>动画的属性。  
  
## <a name="example"></a>示例  
 [!code-xml[BasicAnimations_snippet#AnimationTargetValuesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snippet/CS/AnimationTargetValuesExample.xaml#animationtargetvalueswholepage)]  
  
## <a name="see-also"></a>另请参阅  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [From、 To 和动画目标值示例](http://go.microsoft.com/fwlink/?LinkID=159988)