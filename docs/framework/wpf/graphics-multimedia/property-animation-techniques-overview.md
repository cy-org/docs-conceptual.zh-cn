---
title: "属性动画技术概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "动画, 属性, 方法"
  - "属性, 用于动画处理的方法"
ms.assetid: 74f61413-f8c0-4e75-bf04-951886426c8b
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 属性动画技术概述
本主题描述对属性进行动画处理的不同方法：演示图板、本地动画、时钟以及基于帧的动画。  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## 必备组件  
 若要了解本主题，您应当熟悉[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)中介绍的基本动画功能。  
  
<a name="summary"></a>   
## 不同的动画处理方式  
 由于对属性进行动画处理有多种不同的方案，因此 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 为属性的动画处理提供了多种方法。  
  
 下表指示每种方法是否可基于实例使用；是否可用于样式、控件模板或数据模板；是否可用于 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 以及是否可以使用该方法以交互方式控制动画。  “基于实例”指的是直接将动画或演示图板应用于对象实例（而不是在样式、控件模板或数据模板中应用）的技术。  
  
|动画技术|方案|支持 XAML|可交互控制|  
|----------|--------|-------------|-----------|  
|演示图板动画|基于实例、<xref:System.Windows.Style>、<xref:System.Windows.Controls.ControlTemplate>、<xref:System.Windows.DataTemplate>|是|是|  
|本地动画|基于实例|否|否|  
|时钟动画|基于实例|否|是|  
|基于帧的动画|基于实例|否|不可用|  
  
<a name="storyboard_animations"></a>   
## 演示图板动画  
 在以下情形中使用 <xref:System.Windows.Media.Animation.Storyboard>：要在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中定义并应用动画；在动画开始之后以交互的方式控制动画；创建一个复杂的动画树；或者在 <xref:System.Windows.Style>、<xref:System.Windows.Controls.ControlTemplate> 或 <xref:System.Windows.DataTemplate> 中进行动画处理。  对于需要通过 <xref:System.Windows.Media.Animation.Storyboard> 进行动画处理的对象，它必须是 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement>，或者它必须用于设置 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement>。  有关更多详细信息，请参见[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。  
  
 <xref:System.Windows.Media.Animation.Storyboard> 是一种为其所包含的动画提供目标信息的特殊类型的容器 <xref:System.Windows.Media.Animation.Timeline>。  若要使用 <xref:System.Windows.Media.Animation.Storyboard> 进行动画处理，需要完成下列三个步骤。  
  
1.  声明一个 <xref:System.Windows.Media.Animation.Storyboard> 以及一个或多个动画。  
  
2.  使用 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 和 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A> [附加属性](GTMT)指定每个动画的目标对象和属性。  
  
3.  （仅限代码）为 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 定义一个 <xref:System.Windows.NameScope>。  对将要与该 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 进行动画处理的对象名称进行注册。  
  
4.  启动 <xref:System.Windows.Media.Animation.Storyboard>。  
  
 启动 <xref:System.Windows.Media.Animation.Storyboard> 会将动画应用到它们进行动画处理的属性并将其启动。  启动 <xref:System.Windows.Media.Animation.Storyboard> 的方法有两种：使用 <xref:System.Windows.Media.Animation.Storyboard> 类提供的 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法，或者使用 <xref:System.Windows.Media.Animation.BeginStoryboard> 操作。  在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中进行动画处理的唯一方法是使用 <xref:System.Windows.Media.Animation.BeginStoryboard> 操作。<xref:System.Windows.Media.Animation.BeginStoryboard> 操作可用于 <xref:System.Windows.EventTrigger>、属性 <xref:System.Windows.Trigger> 或 <xref:System.Windows.DataTrigger>。  
  
 下表列出了支持每个 <xref:System.Windows.Media.Animation.Storyboard> 开始技术的不同方面：基于实例、样式、控件模板和数据模板。  
  
|开始演示图板时使用…|基于实例|样式|控件模板|数据模板|示例|  
|----------------|----------|--------|----------|----------|--------|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> 和 <xref:System.Windows.EventTrigger>|是|是|是|是|[使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> 和属性 <xref:System.Windows.Trigger>|否|是|是|是|[在属性值更改时触发动画](../../../../docs/framework/wpf/graphics-multimedia/how-to-trigger-an-animation-when-a-property-value-changes.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> 和 <xref:System.Windows.DataTrigger>|否|是|是|是|[How to: Trigger an Animation When Data Changes](http://msdn.microsoft.com/zh-cn/a736bb3a-2ae5-479a-a33a-75a27055d863)|  
|<xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法|是|否|否|否|[使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)|  
  
 有关 <xref:System.Windows.Media.Animation.Storyboard> 对象的更多信息，请参见[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。  
  
## 本地动画  
 本地动画为对任何 <xref:System.Windows.Media.Animation.Animatable> 对象的[依赖项属性](GTMT)进行动画处理提供了一种简便的方法。  当需要将单个动画应用到属性并且在动画启动后无需以交互方式控制动画时，应使用本地动画。  与 <xref:System.Windows.Media.Animation.Storyboard> 动画不同，本地动画可以对与 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 不相关的对象进行动画处理。  您也不必为此类动画定义 <xref:System.Windows.NameScope>。  
  
 本地动画只能在代码中使用，无法在样式、控件模板或数据模板中进行定义。  本地动画无法在启动后以交互方式控制。  
  
 若要使用本地动画进行动画处理，请完成以下步骤。  
  
1.  创建 <xref:System.Windows.Media.Animation.AnimationTimeline> 对象。  
  
2.  使用需要进行动画处理的对象的 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 方法将 <xref:System.Windows.Media.Animation.AnimationTimeline> 应用到您指定的属性。  
  
 下面的示例演示如何对 <xref:System.Windows.Controls.Button> 的宽度和背景颜色进行动画处理。  
  
 [!code-cpp[animateproperty#11](../../../../samples/snippets/cpp/VS_Snippets_Wpf/animateproperty/CPP/LocalAnimationExample.cpp#11)]
 [!code-csharp[animateproperty#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animateproperty/CSharp/LocalAnimationExample.cs#11)]
 [!code-vb[animateproperty#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animateproperty/VisualBasic/LocalAnimationExample.vb#11)]  
  
## 时钟动画  
 在以下情形中使用 <xref:System.Windows.Media.MediaPlayer.Clock%2A> 对象：在不使用 <xref:System.Windows.Media.Animation.Storyboard> 的情况下需要进行动画处理；在动画启动后需要创建复杂的计时树或需要以交互方式控制动画。  可以使用 Clock 对象对任何 <xref:System.Windows.Media.Animation.Animatable> 对象的[依赖项属性](GTMT)进行动画处理。  
  
 您不能使用 <xref:System.Windows.Media.Animation.Clock> 对象直接在样式、控件模板或数据模板中进行动画处理  （动画和计时系统确实使用 <xref:System.Windows.Media.Animation.Clock> 对象在样式、控件模板或数据模板中进行动画处理，但是它必须从 <xref:System.Windows.Media.Animation.Storyboard> 中为您创建这些 <xref:System.Windows.Media.Animation.Clock> 对象。  有关 <xref:System.Windows.Media.Animation.Storyboard> 对象与 <xref:System.Windows.Media.Animation.Clock> 对象之间的关系的更多信息，请参见[动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)）。  
  
 若要将单个 <xref:System.Windows.Media.Animation.Clock> 应用到属性，请完成以下步骤。  
  
1.  创建 <xref:System.Windows.Media.Animation.AnimationTimeline> 对象。  
  
2.  使用 <xref:System.Windows.Media.Animation.AnimationTimeline> 的 <xref:System.Windows.Media.Animation.AnimationTimeline.CreateClock%2A> 方法来创建 <xref:System.Windows.Media.Animation.AnimationClock>。  
  
3.  使用需要进行动画处理的对象的 <xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%2A> 方法将 <xref:System.Windows.Media.Animation.AnimationClock> 应用到您指定的属性。  
  
 下面的示例演示如何创建一个 <xref:System.Windows.Media.Animation.AnimationClock> 并将其应用到两个相似的属性。  
  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/AnimationClockExample.cs#graphicsmmcreateanimationclockwholeclass)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/animationclockexample.vb#graphicsmmcreateanimationclockwholeclass)]  
  
 若要创建一个计时树并用其对属性进行动画处理，需要完成以下步骤。  
  
1.  使用 <xref:System.Windows.Media.Animation.ParallelTimeline> 和 <xref:System.Windows.Media.Animation.AnimationTimeline> 对象来创建计时树。  
  
2.  使用根 <xref:System.Windows.Media.Animation.ParallelTimeline> 的 <xref:System.Windows.Media.Animation.TimelineGroup.CreateClock%2A> 来创建 <xref:System.Windows.Media.Animation.ClockGroup>。  
  
3.  循环访问 <xref:System.Windows.Media.Animation.ClockGroup> 的 <xref:System.Windows.Media.Animation.ClockGroup.Children%2A> 并应用其 <xref:System.Windows.Media.Animation.Clock> 子对象。  对于每个 <xref:System.Windows.Media.Animation.AnimationClock> 子级，使用需要对其进行动画处理的对象的 <xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%2A> 方法将 <xref:System.Windows.Media.Animation.AnimationClock> 应用到您指定的属性。  
  
 有关 Clock 对象的更多信息，请参见[动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)。  
  
## 基于帧的动画：跳过动画和计时系统  
 当需要完全绕过 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画系统时使用此方法。  此方法的一个方案是物理动画，其中动画中的每一步都需要基于最后一组对象交互重新计算对象。  
  
 基于帧的动画无法在样式、控件模板或数据模板中进行定义。  
  
 若要逐帧进行动画处理，您应注册对象（该对象包含需要进行动画处理的对象）的 <xref:System.Windows.Media.CompositionTarget.Rendering> 事件。  每帧调用一次此事件处理程序方法。  每次 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将[可视化树](GTMT)中持久呈现的数据封送到组合树中时，都将调用事件处理程序方法。  
  
 在事件处理程序中，需要对动画效果执行任意的计算，并设置需要使用这些值进行动画处理的对象的属性。  
  
 若要获取当前帧的显示时间，可以将与此事件相关的 <xref:System.EventArgs> 强制转换为 <xref:System.Windows.Media.RenderingEventArgs>，从而提供可用于获取当前帧呈现时间的 <xref:System.Windows.Media.RenderingEventArgs.RenderingTime%2A> 属性。  
  
 有关更多信息，请参见 <xref:System.Windows.Media.CompositionTarget.Rendering> 页。  
  
## 请参阅  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)   
 [动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)