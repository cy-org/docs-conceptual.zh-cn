---
title: "动画提示和技巧 | Microsoft Docs"
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
  - "对对象进行动画处理 [WPF], 疑难解答"
  - "动画提示和技巧 [WPF]"
  - "动画 [WPF], FillBehavior 属性"
  - "动画 [WPF], 使用系统资源"
  - "性能疑难解答 [WPF], 动画"
  - "提示和技巧 [WPF], 动画"
  - "疑难解答 [WPF], 动画"
  - "动画疑难解答 [WPF]"
ms.assetid: e467796b-d5d4-45a6-a108-8c5d7ff69a0f
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 动画提示和技巧
在处理 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的动画时，可以借助于许多提示和技巧来优化动画的性能并避免出现挫折。  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="generalissuessection"></a>   
## 一般问题  
  
### 对滚动条或滑块的位置进行动画处理会将其冻结  
 如果您使用某个动画对滚动条或滑块的位置进行动画处理，而且该动画的 <xref:System.Windows.Media.Animation.FillBehavior> 为 <xref:System.Windows.Media.Animation.FillBehavior>（默认值），则用户将再也无法移动滚动条或滑块。  原因在于，即使该动画已经结束，它仍将重写目标属性的基值。  若要防止动画重写属性的当前值，请移除它或者为它的 <xref:System.Windows.Media.Animation.FillBehavior> 赋予 <xref:System.Windows.Media.Animation.FillBehavior>。  有关更多信息及示例，请参见[在使用演示图板对属性进行动画处理后设置该属性](../../../../docs/framework/wpf/graphics-multimedia/how-to-set-a-property-after-animating-it-with-a-storyboard.md)。  
  
### 对动画输出进行动画处理不起作用  
 如果某个对象是另一个动画的输出，则不能对该对象进行动画处理。  例如，如果您使用 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> 将 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.Shapes.Shape.Fill%2A> 从 <xref:System.Windows.Media.RadialGradientBrush> 动画处理为 <xref:System.Windows.Media.SolidColorBrush>，则将无法对 <xref:System.Windows.Media.RadialGradientBrush> 或 <xref:System.Windows.Media.SolidColorBrush> 的任何属性进行动画处理。  
  
### 在对属性进行动画处理之后无法更改其值  
 在某些情况下，在对属性进行动画处理之后，即使动画已经结束，似乎也无法更改该属性的值。  原因在于，即使该动画已经结束，它仍在重写该属性的基值。  若要防止动画重写属性的当前值，请移除它或者为它的 <xref:System.Windows.Media.Animation.FillBehavior> 赋予 <xref:System.Windows.Media.Animation.FillBehavior>。  有关更多信息及示例，请参见[在使用演示图板对属性进行动画处理后设置该属性](../../../../docs/framework/wpf/graphics-multimedia/how-to-set-a-property-after-animating-it-with-a-storyboard.md)。  
  
### 更改时间线不起作用  
 尽管大部分 <xref:System.Windows.Media.Animation.Timeline> 属性是可以进行动画处理和数据绑定的，但是更改处于活动状态的 <xref:System.Windows.Media.Animation.Timeline> 的属性值似乎不起作用。  原因在于，当 <xref:System.Windows.Media.Animation.Timeline> 开始时，计时系统会创建 <xref:System.Windows.Media.Animation.Timeline> 的一个副本，并使用该副本来创建一个 <xref:System.Windows.Media.Animation.Clock> 对象。  修改原始对象不会影响到计时系统所创建的副本。  
  
 为了使 <xref:System.Windows.Media.Animation.Timeline> 反映所做的更改，必须重新生成它的时钟，并使用该时钟来替换以前创建的时钟。  系统不会为您自动生成时钟。  下面是应用时间线更改的几种方法：  
  
-   如果时间线为 <xref:System.Windows.Media.Animation.Storyboard> 或属于它，则可以使用 <xref:System.Windows.Media.Animation.BeginStoryboard> 或 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法重新应用时间线的演示图板，从而使时间线反映更改。  这会带来副作用，即还会重新启动动画。  在代码中，可以使用 <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> 方法将演示图板向前移回到其上一位置。  
  
-   如果使用 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 方法将动画直接应用于属性，请再次调用 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 方法并将修改后的动画传递给此方法。  
  
-   如果直接在时钟级别操作，请创建并应用一组新时钟，然后用它们来替换以前生成的那组时钟。  
  
 有关时间线和时钟的更多信息，请参见[动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)。  
  
### FillBehavior.Stop 不按照预期方式工作  
 有时，将 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 属性设置为 <xref:System.Windows.Media.Animation.FillBehavior>（例如，将一个动画“切换”到另一个动画时）似乎不起作用，因为它的 <xref:System.Windows.Media.Animation.HandoffBehavior> 具有 <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A> 设置。  
  
 下面的示例创建一个 <xref:System.Windows.Controls.Canvas>、<xref:System.Windows.Shapes.Rectangle> 和 <xref:System.Windows.Media.TranslateTransform>。  将对 <xref:System.Windows.Media.TranslateTransform> 进行动画处理，以便在 <xref:System.Windows.Controls.Canvas> 中到处移动 <xref:System.Windows.Shapes.Rectangle>。  
  
 [!code-xml[AnimationTipsAndTricksSample_snip#FillBehaviorTipAnimatedObject](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipanimatedobject)]  
  
 本节中的示例使用前面的对象来演示 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 属性不能按预期方式工作的几种情况。  
  
#### 针对多个动画的 FillBehavior\="Stop" 和 HandoffBehavior  
 有时，当某个动画由另一个动画替换时，似乎会忽略第一个动画的 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 属性。  请看下面的示例，该示例创建了两个 <xref:System.Windows.Media.Animation.Storyboard> 对象并使用它们对前一示例中所显示的同一个 <xref:System.Windows.Media.TranslateTransform> 进行动画处理。  
  
 第一个 <xref:System.Windows.Media.Animation.Storyboard> \(`B1`\) 将 <xref:System.Windows.Media.TranslateTransform> 的 <xref:System.Windows.Media.TranslateTransform.X%2A> 属性从 0 动画处理为 350，这会将该矩形向右移动 350 个像素。  当动画达到其持续时间的末尾并停止播放时，<xref:System.Windows.Media.TranslateTransform.X%2A> 属性会恢复到其原始值 0。  因此，该矩形会在向右移动 350 个像素之后跳回至其原始位置。  
  
 [!code-xml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardB1Button](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardb1button)]  
  
 第二个 <xref:System.Windows.Media.Animation.Storyboard> \(`B2`\) 也是对同一个 <xref:System.Windows.Media.TranslateTransform> 的 <xref:System.Windows.Media.TranslateTransform.X%2A> 属性进行动画处理。  由于为该 <xref:System.Windows.Media.Animation.Storyboard> 中的动画仅设置了 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性，因此，该动画将它进行动画处理的属性的当前值作为其起始值。  
  
 [!code-xml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardB2Button](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardb2button)]  
  
 如果您在第一个 <xref:System.Windows.Media.Animation.Storyboard> 正在播放时单击第二个按钮，则可能会遇到下面的行为：  
  
1.  第一个演示图板结束该矩形的动画播放并使其回到其初始位置，因为该动画的 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 为 <xref:System.Windows.Media.Animation.FillBehavior>。  
  
2.  第二个演示图板生效并从当前位置（现在为 0）动画处理为 500。  
  
 **但实际情况并非如此。**该矩形并没有跳回至初始位置，而是继续向右移动。  这是由于第二个动画使用第一个动画的当前值作为其起始值，并在该值与 500 之间进行动画处理。  当由于使用 <xref:System.Windows.Media.Animation.HandoffBehavior> <xref:System.Windows.Media.Animation.HandoffBehavior> 而将第一个动画替换为第二个动画时，第一个动画的 <xref:System.Windows.Media.Animation.FillBehavior> 将不起作用。  
  
#### FillBehavior 和 Completed 事件  
 随后的几个示例演示 <xref:System.Windows.Media.Animation.FillBehavior> <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 似乎不起作用的另一个情形。  该示例也是使用演示图板将 <xref:System.Windows.Media.TranslateTransform> 的 <xref:System.Windows.Media.TranslateTransform.X%2A> 属性从 0 到 350 进行动画处理。  但是，这一次，该示例会注册 <xref:System.Windows.Media.Animation.Timeline.Completed> 事件。  
  
 [!code-xml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardCButton](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardcbutton)]  
  
 <xref:System.Windows.Media.Animation.Timeline.Completed> 事件处理程序启动另一个 <xref:System.Windows.Media.Animation.Storyboard>，该演示图板将同一个属性从其当前值动画处理为 500。  
  
 [!code-csharp[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardC1CompletedHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml.cs#fillbehaviortipstoryboardc1completedhandler)]
 [!code-vb[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardC1CompletedHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/VisualBasic/FillBehaviorTip.xaml.vb#fillbehaviortipstoryboardc1completedhandler)]  
  
 下面是用来将第二个 <xref:System.Windows.Media.Animation.Storyboard> 定义为资源的标记。  
  
 [!code-xml[AnimationTipsAndTricksSample_snip#FillBehaviorTipResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipresources)]  
  
 当您运行 <xref:System.Windows.Media.Animation.Storyboard> 时，您可能希望 <xref:System.Windows.Media.TranslateTransform> 的 <xref:System.Windows.Media.TranslateTransform.X%2A> 属性从 0 到 350 进行动画处理，然后在完成之后回到 0（因为它的 <xref:System.Windows.Media.Animation.FillBehavior> 设置为 <xref:System.Windows.Media.Animation.FillBehavior>），最后再将该属性从 0 到 500 进行动画处理。  相反，<xref:System.Windows.Media.TranslateTransform> 将从 0 到 350 进行动画处理，然后再动画处理到 500。  
  
 这是由于 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 按照一定的顺序引发事件，而且除非该属性无效，否则属性值将缓存起来而且将不重新计算。  <xref:System.Windows.Media.Animation.Timeline.Completed> 事件将首先处理，因为它是由根时间线（第一个 <xref:System.Windows.Media.Animation.Storyboard>）触发的。  此时，<xref:System.Windows.Media.TranslateTransform.X%2A> 属性仍返回其动画值，因为它尚且有效。  第二个 <xref:System.Windows.Media.Animation.Storyboard> 使用缓存值作为其起始值并开始进行动画处理。  
  
<a name="performancesection"></a>   
## 性能  
  
### 在离开页面时其中的动画继续运行  
 当您离开包含正在运行的动画的 <xref:System.Windows.Controls.Page> 时，这些动画将继续播放，直到对 <xref:System.Windows.Controls.Page> 进行垃圾回收。  根据所使用的导航系统，离开的页面可能会在内存中无限期保留，其动画将一直占用资源。  当页面中包含不断运行的（“环境”）动画时，此问题尤为突出。  
  
 因此，在离开页面时，最好使用 <xref:System.Windows.FrameworkElement.Unloaded> 事件来移除动画。  
  
 可通过不同的方法移除动画。  可以使用下列方法来移除属于 <xref:System.Windows.Media.Animation.Storyboard> 的动画。  
  
-   若要移除用事件触发器启动的 <xref:System.Windows.Media.Animation.Storyboard>，请参见[How to: Remove a Storyboard](http://msdn.microsoft.com/zh-cn/7fe39531-de2f-46a0-a69f-b783d04235ee)。  
  
-   若要使用代码来移除 <xref:System.Windows.Media.Animation.Storyboard>，请参见 <xref:System.Windows.Media.Animation.Storyboard.Remove%2A> 方法。  
  
 无论动画的启动方式如何，都可以使用下面的方法。  
  
-   若要从特定的属性中移除动画，请使用 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29> 方法。  将正在进行动画处理的属性指定为第一个参数，将 `null` 指定为第二个参数。  这将从属性中移除所有动画时钟。  
  
 有关用来对属性进行动画处理的不同方法的更多信息，请参见[属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)。  
  
### 使用组合 HandoffBehavior 会占用系统资源  
 使用 <xref:System.Windows.Media.Animation.HandoffBehavior> <xref:System.Windows.Media.Animation.HandoffBehavior> 将 <xref:System.Windows.Media.Animation.Storyboard>、<xref:System.Windows.Media.Animation.AnimationTimeline> 或 <xref:System.Windows.Media.Animation.AnimationClock> 应用到某个属性时，以前与该属性关联的任何 <xref:System.Windows.Media.Animation.Clock> 对象都会继续占用系统资源；计时系统不会自动移除这些时钟。  
  
 在使用 <xref:System.Windows.Media.Animation.HandoffBehavior> 应用大量时钟时，若要避免出现性能问题，应在时钟应用完成后从经过动画处理的属性中移除组合时钟。  可用来移除时钟的方法有若干种。  
  
-   若要从属性中移除所有时钟，请使用经过动画处理的对象的 <xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationClock%29> 或 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29> 方法。  将正在进行动画处理的属性指定为第一个参数，将 `null` 指定为第二个参数。  这将从属性中移除所有动画时钟。  
  
-   若要从时钟列表中移除特定的 <xref:System.Windows.Media.Animation.AnimationClock>，请使用 <xref:System.Windows.Media.Animation.AnimationClock> 的 <xref:System.Windows.Media.Animation.Clock.Controller%2A> 属性来检索 <xref:System.Windows.Media.Animation.ClockController>，然后调用 <xref:System.Windows.Media.Animation.ClockController> 的 <xref:System.Windows.Media.Animation.ClockController.Remove%2A> 方法。  这通常是在时钟的 <xref:System.Windows.Media.Animation.Clock.Completed> 事件处理程序中完成的。  请注意，<xref:System.Windows.Media.Animation.ClockController> 只能控制根时钟；子时钟的 <xref:System.Windows.Media.Animation.Clock.Controller%2A> 属性将返回 `null`。  另请注意，如果时钟的有效持续时间为无限长，则不会调用 <xref:System.Windows.Media.Animation.Clock.Completed> 事件。  在这种情况下，用户将需要确定何时调用 <xref:System.Windows.Media.Animation.ClockController.Remove%2A>。  
  
 这主要是生存期很长的对象上的动画所具有的问题。  将对象作为垃圾回收时，同时将断开其时钟的连接并将其时钟作为垃圾回收。  
  
 有关时钟对象的更多信息，请参见[动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)。  
  
## 请参阅  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)