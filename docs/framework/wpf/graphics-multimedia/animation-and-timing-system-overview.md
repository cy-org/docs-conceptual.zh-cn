---
title: "动画和计时系统概述 | Microsoft Docs"
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
  - "动画 [WPF]"
  - "计时系统 [WPF]"
ms.assetid: 172cd5a8-a333-4c81-9456-fafccc19f382
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 动画和计时系统概述
本主题描述计时系统如何使用动画、<xref:System.Windows.Media.Animation.Timeline> 和 <xref:System.Windows.Media.Animation.Clock> 类来对属性进行动画处理。  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## 必备组件  
 为了了解本主题，您应当能够使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画来对属性进行动画处理，如[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)所述。  本主题还有助于您熟悉[依赖项属性](GTMT)；有关更多信息，请参见[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  
  
<a name="timelinesandclocks"></a>   
## 时间线和时钟  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)描述了 <xref:System.Windows.Media.Animation.Timeline> 如何表示一个时间段，还描述了动画是生成输出值的某种类型的 <xref:System.Windows.Media.Animation.Timeline>。  <xref:System.Windows.Media.Animation.Timeline> 本身除了仅仅描述一个时间段外，不执行任何其他操作。  实际工作是由时间线的 <xref:System.Windows.Media.Animation.Clock> 对象执行的。  同样，动画实际上不对属性进行动画处理：动画类描述应如何计算输出值，但它是为某个动画创建的 <xref:System.Windows.Media.Animation.Clock>，该动画会促进动画输出并将其应用于属性。  
  
 <xref:System.Windows.Media.Animation.Clock> 是一种特殊类型的对象，它维护 <xref:System.Windows.Media.Animation.Timeline> 的与计时相关的运行时状态。  它提供动画和计时系统所必需的三则信息：<xref:System.Windows.Media.Animation.Clock.CurrentTime%2A>、<xref:System.Windows.Media.Animation.Clock.CurrentProgress%2A> 和 <xref:System.Windows.Media.Animation.Clock.CurrentState%2A>。  <xref:System.Windows.Media.Animation.Clock> 使用由它的 <xref:System.Windows.Media.Animation.Timeline> 所描述的计时行为（<xref:System.Windows.Media.Animation.Timeline.Duration%2A>、<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 和 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 等）来确定它的当前时间、进度和状态。  
  
 在多数情况下，会自动为您的时间线创建一个 <xref:System.Windows.Media.Animation.Clock>。  当您使用 <xref:System.Windows.Media.Animation.Storyboard> 或 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 方法来进行动画处理时，系统会自动为您的时间线和动画创建时钟，并将这些时钟应用于其目标属性。  您还可以使用 <xref:System.Windows.Media.Animation.Timeline> 的 <xref:System.Windows.Media.Animation.Timeline.CreateClock%2A> 方法显式创建 <xref:System.Windows.Media.Animation.Clock>。  <xref:System.Windows.Media.MediaTimeline.CreateClock%2A?displayProperty=fullName> 方法为调用它的 <xref:System.Windows.Media.Animation.Timeline> 创建适当类型的时钟。  如果 <xref:System.Windows.Media.Animation.Timeline> 包含子时间线，则还会为这些子时间线创建 <xref:System.Windows.Media.Animation.Clock> 对象。  所得到的 <xref:System.Windows.Media.Animation.Clock> 对象将以树的形式排列，这些树与这些对象创建时所在的 <xref:System.Windows.Media.Animation.Timeline> 对象树相匹配。  
  
 不同类型的时间线具有不同类型的时钟。  下表显示的是与一些不同 <xref:System.Windows.Media.Animation.Timeline> 类型相对应的 <xref:System.Windows.Media.Animation.Clock> 类型。  
  
|时间线类型|时钟类型|时钟用途|  
|-----------|----------|----------|  
|动画（继承自 <xref:System.Windows.Media.Animation.AnimationTimeline>）|<xref:System.Windows.Media.Animation.AnimationClock>|为依赖项属性生成输出值。|  
|<xref:System.Windows.Media.MediaTimeline>|<xref:System.Windows.Media.MediaClock>|处理媒体文件。|  
|<xref:System.Windows.Media.Animation.ParallelTimeline>|<xref:System.Windows.Media.Animation.ClockGroup>|对它的子 <xref:System.Windows.Media.Animation.Clock> 对象进行分组和控制|  
|<xref:System.Windows.Media.Animation.Storyboard>|<xref:System.Windows.Media.Animation.ClockGroup>|对它的子 <xref:System.Windows.Media.Animation.Clock> 对象进行分组和控制|  
  
 可以使用 <xref:System.Windows.Media.Animation.IAnimatable.ApplyAnimationClock%2A> 方法，将您创建的任何 <xref:System.Windows.Media.Animation.AnimationClock> 对象应用于兼容的依赖项属性。  
  
 在严重依赖性能的方案（如对大量类似的对象进行动画处理）中，管理您自己对 <xref:System.Windows.Media.Animation.Clock> 的使用可能会提高性能。  
  
<a name="timemanager"></a>   
## 时钟和时间管理器  
 当您对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的对象进行动画处理时，时间管理器会管理系统为您的时间线创建的 <xref:System.Windows.Media.MediaPlayer.Clock%2A> 对象。  时间管理器是 <xref:System.Windows.Media.MediaPlayer.Clock%2A> 对象树的根，并控制该树中的时间流。  时间管理器是为每个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序自动创建的，它对于应用程序开发人员不可见。时间管理器每秒钟“滴答”多次；实际滴答次数取决于可用的系统资源。  在每个滴答过程中，时间管理器都会计算计时树中所有 <xref:System.Windows.Media.Animation.ClockState> <xref:System.Windows.Media.Animation.Clock> 对象的状态。  
  
 下图演示时间管理器、<xref:System.Windows.Media.Animation.AnimationClock> 和带有动画的依赖项属性之间的关系。  
  
 ![计时系统组件](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-clocks-1clock1prop.png "graphicsmm\_clocks\_1clock1prop")  
对属性进行动画处理  
  
 当时间管理器滴答时，它会更新应用程序中每个 <xref:System.Windows.Media.Animation.ClockState> <xref:System.Windows.Media.Animation.Clock> 的时间。  如果 <xref:System.Windows.Media.Animation.Clock> 是 <xref:System.Windows.Media.Animation.AnimationClock>，它会使用从中创建它的 <xref:System.Windows.Media.Animation.AnimationTimeline> 的 <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> 方法来计算其当前的输出值。  <xref:System.Windows.Media.Animation.AnimationClock> 向 <xref:System.Windows.Media.Animation.AnimationTimeline> 提供当前的本地时间、一个输入值（通常是属性的基值）和一个默认目标值。  当您使用 <xref:System.Windows.DependencyObject.GetValue%2A> 方法或动画依据属性的 CLR 访问器检索该属性的值时，会获得该属性的 <xref:System.Windows.Media.Animation.AnimationClock> 的输出。  
  
#### 时钟组  
 上一节描述了不同类型的时间线具有不同类型的 <xref:System.Windows.Media.Animation.Clock> 对象。  下图演示时间管理器、<xref:System.Windows.Media.Animation.ClockGroup>、<xref:System.Windows.Media.Animation.AnimationClock> 和带有动画的依赖项属性之间的关系。  <xref:System.Windows.Media.Animation.ClockGroup> 是为用来对其他时间线进行分组的时间线创建的，如 <xref:System.Windows.Media.Animation.Storyboard> 类，该类对动画和其他时间线进行分组。  
  
 ![计时系统组件](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-clocks-2clock1clockgroup2prop.png "graphicsmm\_clocks\_2clock1clockgroup2prop")  
ClockGroup  
  
#### Composition  
 可以将多个时钟与一个属性相关联，在这种情况下，每个时钟都将上一个时钟的输出值用作其基值。  下图演示的是应用于同一个属性的三个 <xref:System.Windows.Media.Animation.AnimationClock> 对象。  时钟1 将动画属性的基值用作其输入，并使用该值来生成输出。  时钟2 将时钟1 的输出用作其输入，并使用该值来生成输出。  时钟3 将时钟2 的输出用作其输入，并使用该值来生成输出。  如果多个时钟同时影响同一个属性，则认为这些时钟位于一个结构链中。  
  
 ![计时系统组件](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-clocks-2clock1prop.png "graphicsmm\_clocks\_2clock1prop")  
结构链  
  
 请注意，尽管在结构链中 <xref:System.Windows.Media.Animation.AnimationClock> 对象的输入和输出之间创建了关系，但是这些对象的计时行为不会受到影响；<xref:System.Windows.Media.Animation.Clock> 对象（包括 <xref:System.Windows.Media.Animation.AnimationClock> 对象）对于它们的父级 <xref:System.Windows.Media.Animation.Clock> 对象具有分层依赖性。  
  
 若要对同一个属性应用多个时钟，在应用 <xref:System.Windows.Media.Animation.Storyboard>、动画或 <xref:System.Windows.Media.Animation.AnimationClock> 时，请使用 <xref:System.Windows.Media.Animation.HandoffBehavior> <xref:System.Windows.Media.Animation.HandoffBehavior>。  
  
#### 滴答和事件合并  
 除了计算输出值以外，时间管理器还会在它每走过一个刻度时执行其他工作：它会确定每个时钟的状态并在适当时引发事件。  
  
 尽管滴答频率很高，但是在两次滴答之间还是有可能会发生许多事情。  例如，<xref:System.Windows.Media.Animation.Clock> 可能会停止、启动和再次停止，在这种情况下，它的 <xref:System.Windows.Media.Animation.Clock.CurrentState%2A> 值将更改三次。  理论上，<xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> 事件可以在一个滴答过程中引发多次；但是，计时引擎会对事件进行合并，因此，在每个滴答过程中，最多只能引发 <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> 事件一次。  这同样适用于所有的计时事件：对于给定的 <xref:System.Windows.Media.Animation.Clock> 对象，针对每种类型最多引发一个事件。  
  
 当 <xref:System.Windows.Media.Animation.Clock> 在两次滴答之间切换状态并恢复到最初的状态（如从 <xref:System.Windows.Media.Animation.ClockState> 更改为 <xref:System.Windows.Media.Animation.ClockState>，然后再恢复为 <xref:System.Windows.Media.Animation.ClockState>）时，仍将发生相关的事件。  
  
 有关计时事件的更多信息，请参见[计时事件概述](../../../../docs/framework/wpf/graphics-multimedia/timing-events-overview.md)。  
  
<a name="currentvaluesbasevaluesofproperties"></a>   
## 属性的当前值和基值  
 可进行动画处理的属性可以具有两个值：基值和当前值。  当您使用属性的 CLR 访问器或 <xref:System.Windows.DependencyObject.SetValue%2A> 方法设置属性时，可以设置属性的基值。  对于尚未动画处理的属性，基值和当前值是相等的。  
  
 当您对属性进行动画处理时，<xref:System.Windows.Media.Animation.AnimationClock> 会设置属性的*当前* 值。  当 <xref:System.Windows.Media.Animation.AnimationClock> 为 <xref:System.Windows.Media.Animation.ClockState> 或 <xref:System.Windows.Media.Animation.ClockState> 时，通过属性的 CLR 访问器或 <xref:System.Windows.DependencyObject.GetValue%2A> 方法检索属性值会返回 <xref:System.Windows.Media.Animation.AnimationClock> 的输出。  可以使用 <xref:System.Windows.Media.Animation.IAnimatable.GetAnimationBaseValue%2A> 方法来检索属性的基值。  
  
## 请参阅  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [计时事件概述](../../../../docs/framework/wpf/graphics-multimedia/timing-events-overview.md)   
 [计时行为概述](../../../../docs/framework/wpf/graphics-multimedia/timing-behaviors-overview.md)