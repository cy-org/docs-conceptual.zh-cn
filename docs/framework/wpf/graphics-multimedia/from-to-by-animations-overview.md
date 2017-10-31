---
title: "From/To/By 动画概述 | Microsoft Docs"
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
  - "动画, From/to/by"
  - "From/to/by 动画"
ms.assetid: 516fce0a-e7f8-49b8-b018-53b3d409a8a3
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# From/To/By 动画概述
本主题描述如何使用 From\/To\/By 动画对[依赖项属性](GTMT)进行动画处理。  From\/To\/By 动画创建两个值之间的过渡。  
  
 本主题包括以下部分。  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prereq"></a>   
## 必备组件  
 若要了解本主题，您应当熟悉 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画功能。  有关动画功能的简介，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
<a name="whatisanimation"></a>   
## 什么是 From\/To\/By 动画  
 From\/To\/By 动画是一种 <xref:System.Windows.Media.Animation.AnimationTimeline> 类型，它创建起始值和结束值之间的过渡。  完成过渡所需的时间由该动画的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 确定。  
  
 可以通过在标记和代码中使用 <xref:System.Windows.Media.Animation.Storyboard>，或在代码中使用 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 方法，将 From\/To\/By 动画应用于属性。  还可以使用 From\/To\/By 动画创建 <xref:System.Windows.Media.Animation.AnimationClock>，并将其应用于一个或多个属性。  有关应用动画的各种方法的更多信息，请参见[属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)。  
  
 From\/To\/By 动画的目标值不能超过两个。  如果需要具有两个以上目标值的动画，请使用关键帧动画。  [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)中描述了关键帧动画。  
  
<a name="animation_types"></a>   
## From\/To\/By 动画类型  
 由于动画生成属性值，因此对于不同的属性类型，会有不同的动画类型。  若要对采用 <xref:System.Double> 的属性（例如元素的 <xref:System.Windows.FrameworkElement.Width%2A> 属性）进行动画处理，请使用生成 <xref:System.Double> 值的动画。  若要对采用 <xref:System.Windows.Point> 的属性进行动画处理，请使用生成 <xref:System.Windows.Point> 值的动画，依此类推。  
  
 From\/To\/By 动画类属于 <xref:System.Windows.Media.Animation> 命名空间，并使用下列命名约定：  
  
 *\<类型\>* `Animation`  
  
 其中 *\<类型\>* 是该类进行动画处理的值的类型。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供下列 From\/To\/By 动画类。  
  
|属性类型|对应的 From\/To\/By 动画类|  
|----------|--------------------------|  
|<xref:System.Byte>|<xref:System.Windows.Media.Animation.ByteAnimation>|  
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimation>|  
|<xref:System.Decimal>|<xref:System.Windows.Media.Animation.DecimalAnimation>|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimation>|  
|<xref:System.Int16>|<xref:System.Windows.Media.Animation.Int16Animation>|  
|<xref:System.Int32>|<xref:System.Windows.Media.Animation.Int32Animation>|  
|<xref:System.Int64>|<xref:System.Windows.Media.Animation.Int64Animation>|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimation>|  
|<xref:System.Windows.Media.Media3D.Quaternion>|<xref:System.Windows.Media.Animation.QuaternionAnimation>|  
|<xref:System.Windows.Rect>|<xref:System.Windows.Media.Animation.RectAnimation>|  
|<xref:System.Windows.Media.Media3D.Rotation3D>|<xref:System.Windows.Media.Animation.Rotation3DAnimation>|  
|<xref:System.Single>|<xref:System.Windows.Media.Animation.SingleAnimation>|  
|<xref:System.Windows.Size>|<xref:System.Windows.Media.Animation.SizeAnimation>|  
|<xref:System.Windows.Thickness>|<xref:System.Windows.Media.Animation.ThicknessAnimation>|  
|<xref:System.Windows.Media.Media3D.Vector3D>|<xref:System.Windows.Media.Animation.Vector3DAnimation>|  
|<xref:System.Windows.Vector>|<xref:System.Windows.Media.Animation.VectorAnimation>|  
  
<a name="anim_values"></a>   
## 目标值  
 From\/To\/By 动画创建两个目标值之间的过渡。  通常是指定一个起始值（使用 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性来设置）和一个结束值（使用 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性来设置）。  但是，也可以只指定起始值、目标值或偏移量值。  此时，动画从正在进行动画处理的属性获取缺少的目标值。  以下列表描述了指定动画目标值的各种方法。  
  
-   **起始值**  
  
     如果要显式指定动画的起始值，请使用 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性。  可以只使用 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性自身，也可以将该属性与 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 或 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性一起使用。  如果只指定 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性，则动画从该值过渡到进行动画处理的属性的基值。  
  
-   **结束值**  
  
     若要指定动画的结束值，请使用其 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性。  如果只使用 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性自身，则动画从正在进行动画处理的属性获取其起始值，或者从应用于同一属性的另一个动画的输出获取其起始值。  可以将 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性与 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性一起使用，以显式指定动画的起始值和结束值。  
  
-   **偏移量值**  
  
     可以使用 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性指定动画的偏移量，而不指定显式起始值或结束值。  动画的 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性指定动画在其持续期间更改某值的程度。  可以只使用 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性自身，也可以将该属性与 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性一起使用。  如果只指定 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性，则动画将偏移量值添加到该属性的基值或另一个动画的输出。  
  
<a name="examples"></a>   
## 使用 From\/To\/By 值  
 下面的部分介绍如何一起或单独使用 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>、<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 和 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性。  
  
 本部分中的每个示例都使用 <xref:System.Windows.Media.Animation.DoubleAnimation>（From\/To\/By 动画的一种类型）对一个高度为 10 个[与设备无关的像素](GTMT)、宽度为 100 个[与设备无关的像素](GTMT) 的 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.FrameworkElement.Width%2A> 属性进行动画处理。  
  
 虽然每个示例都使用 <xref:System.Windows.Media.Animation.DoubleAnimation>，但所有 From\/To\/By 动画的 From、To 和 By 属性的行为都相同。  虽然每个示例都使用 <xref:System.Windows.Media.Animation.Storyboard>，不过也可以通过其他方式使用 From\/To\/By 动画。  有关更多信息，请参见[属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)。  
  
### From\/To  
 如果同时设置了 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 和 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 值，则动画从 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性指定的值继续到 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性指定的值。  
  
 下面的示例将 <xref:System.Windows.Media.Animation.DoubleAnimation> 的 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性设置为 50，并将其 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性设置为 300。  结果，<xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.FrameworkElement.Width%2A> 以动画形式从 50 过渡到 300。  
  
 [!code-csharp[basicvalues_snip#FromToAnimationInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#fromtoanimationinline)]
 [!code-vb[basicvalues_snip#FromToAnimationInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#fromtoanimationinline)]  
  
### 若要  
 如果只设置 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性，则动画从进行动画处理的属性的基值，或以前应用于同一属性的组合动画的输出，继续到 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性指定的值。  
  
 （“组合动画”是指以前应用于同一属性、在使用 <xref:System.Windows.Media.Animation.HandoffBehavior> 提交行为应用当前动画时仍然有效的 <xref:System.Windows.Media.Animation.ClockState> 或 <xref:System.Windows.Media.Animation.ClockState> 动画）。  
  
 下面的示例只将 <xref:System.Windows.Media.Animation.DoubleAnimation> 的 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性设置为 300。  由于未指定起始值，因此 <xref:System.Windows.Media.Animation.DoubleAnimation> 使用 <xref:System.Windows.FrameworkElement.Width%2A> 属性的基值 \(100\) 作为其起始值。  <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.FrameworkElement.Width%2A> 以动画形式从 100 过渡到动画的目标值 300。  
  
 [!code-csharp[basicvalues_snip#ToAnimationInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#toanimationinline)]
 [!code-vb[basicvalues_snip#ToAnimationInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#toanimationinline)]  
  
### By  
 如果只设置动画的 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性，则动画从正在进行动画处理的属性的基值，或组合动画的输出，继续到该值与 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性指定的值之和。  
  
 下面的示例只将 <xref:System.Windows.Media.Animation.DoubleAnimation> 的 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性设置为 300。  由于该示例未指定起始值，因此 <xref:System.Windows.Media.Animation.DoubleAnimation> 使用 <xref:System.Windows.FrameworkElement.Width%2A> 属性的基值 100 作为其起始值。  结束值通过将动画的 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 值 300 与其起始值 100 相加而得到 400。  因此，<xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.FrameworkElement.Width%2A> 以动画形式从 100 过渡到 400。  
  
 [!code-csharp[basicvalues_snip#ByAnimationInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#byanimationinline)]
 [!code-vb[basicvalues_snip#ByAnimationInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#byanimationinline)]  
  
### From\/By  
 如果设置了动画的 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 和 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性，则动画从 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性指定的值，继续到由 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 和 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性之和指定的值。  
  
 下面的示例将 <xref:System.Windows.Media.Animation.DoubleAnimation> 的 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性设置为 50，并将其 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性设置为 300。  结束值通过将动画的 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 值 300 与其起始值 50 相加而得到 350。  因此，<xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.FrameworkElement.Width%2A> 以动画形式从 50 过渡到 350。  
  
 [!code-csharp[basicvalues_snip#FromByAnimationInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#frombyanimationinline)]
 [!code-vb[basicvalues_snip#FromByAnimationInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#frombyanimationinline)]  
  
### 发件人  
 如果只指定动画的 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 值，则动画从 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性指定的值，继续到正在进行动画处理的属性的基值，或组合动画的输出。  
  
 下面的示例只将 <xref:System.Windows.Media.Animation.DoubleAnimation> 的 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性设置为 50。  由于未指定结束值，因此 <xref:System.Windows.Media.Animation.DoubleAnimation> 使用 <xref:System.Windows.FrameworkElement.Width%2A> 属性的基值 100 作为其结束值。  <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.FrameworkElement.Width%2A> 以动画形式从 50 过渡到 <xref:System.Windows.FrameworkElement.Width%2A> 属性的基值 100。  
  
 [!code-csharp[basicvalues_snip#FromAnimationInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#fromanimationinline)]
 [!code-vb[basicvalues_snip#FromAnimationInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#fromanimationinline)]  
  
### To\/By  
 如果同时设置了动画的 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 和 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性，则忽略 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> 属性。  
  
<a name="otheranimationtypes"></a>   
## 其他动画类型  
 From\/To\/By 动画不是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供的唯一动画类型，它还提供了关键帧动画和路径动画。  
  
-   关键帧动画沿着用关键帧所描述的任意数量的目标值进行动画处理。  有关更多信息，请参见 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)。  
  
-   路径动画从 <xref:System.Windows.Media.PathGeometry> 生成输出值。  有关更多信息，请参见 [路径动画概述](../../../../docs/framework/wpf/graphics-multimedia/path-animations-overview.md)。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还允许您创建自己的自定义动画类型。  有关更多信息，请参见 [自定义动画概述](../../../../docs/framework/wpf/graphics-multimedia/custom-animations-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.Timeline>   
 <xref:System.Windows.Media.Animation.Storyboard>   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [路径动画概述](../../../../docs/framework/wpf/graphics-multimedia/path-animations-overview.md)   
 [自定义动画概述](../../../../docs/framework/wpf/graphics-multimedia/custom-animations-overview.md)   
 [From, To, and By Animation Target Values Sample](http://go.microsoft.com/fwlink/?LinkID=159988)