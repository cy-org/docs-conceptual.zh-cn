---
title: "计时行为概述 | Microsoft Docs"
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
  - "行为, 计时"
  - "计时行为"
ms.assetid: 5b714d46-bd46-48b8-b467-b4be89ba3091
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 计时行为概述
本主题描述动画和其他 <xref:System.Windows.Media.Animation.Timeline> 对象的计时行为。  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## 必备组件  
 若要了解本主题，您应当熟悉基本动画功能。  有关更多信息，请参见 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
<a name="timelinetypes"></a>   
## 时间线类型  
 <xref:System.Windows.Media.Animation.Timeline> 表示一个时间段。  它提供的属性可以让您指定该时间段的长度、开始时间、重复次数、该时间段内时间进度的快慢等等。  
  
 从时间线类继承的类可提供附加功能，例如动画和媒体播放。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供以下 <xref:System.Windows.Media.Animation.Timeline> 类型：  
  
|时间线类型|说明|  
|-----------|--------|  
|<xref:System.Windows.Media.Animation.AnimationTimeline>|<xref:System.Windows.Media.Animation.Timeline> 对象（这些对象生成输出值以对属性进行动画处理）的抽象基类。|  
|<xref:System.Windows.Media.MediaTimeline>|从媒体文件生成输出。|  
|<xref:System.Windows.Media.Animation.ParallelTimeline>|一种 <xref:System.Windows.Media.Animation.TimelineGroup>，对子 <xref:System.Windows.Media.Animation.Timeline> 对象进行分组和控制。|  
|<xref:System.Windows.Media.Animation.Storyboard>|一种 <xref:System.Windows.Media.Animation.ParallelTimeline>，为其包含的 Timeline 对象提供目标信息。|  
|<xref:System.Windows.Media.Animation.Timeline>|定义计时行为的抽象基类。|  
|<xref:System.Windows.Media.Animation.TimelineGroup>|可包含其他 <xref:System.Windows.Media.Animation.Timeline> 对象的 <xref:System.Windows.Media.Animation.Timeline> 对象的抽象类。|  
  
<a name="propertiesthatcontroltimelinelength"></a>   
## 用于控制时间线长度的属性  
 <xref:System.Windows.Media.Animation.Timeline> 表示一个时间段，时间线的长度可以用不同的方法描述。  下表定义了几个用于描述时间线长度的术语。  
  
|术语|说明|属性||||  
|--------|--------|--------|-|-|-|  
|简单持续时间|时间线向前迭代一次所花费的时间长度。|<xref:System.Windows.Media.Animation.Timeline.Duration%2A>||||  
|一次重复|时间线向前播放一次所花费的时间长度，如果 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 属性为 True，则是倒退一次的时间长度。|<xref:System.Windows.Media.Animation.Timeline.Duration%2A>, <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>||||  
|活动期|时间线完成所有由其 <xref:System.Windows.Media.Animation.RepeatBehavior> 属性指定的重复所花费的时间长度。|<xref:System.Windows.Media.Animation.Timeline.Duration%2A>, <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>, <xref:System.Windows.Media.Animation.RepeatBehavior>||||  
  
<a name="duration"></a>   
### Duration 属性  
 如前文所述，时间线代表一个时间段。  该时间段的长度由时间线的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 属性确定。  当时间线达到其持续时间的终点时，就会停止播放。  如果该时间线具有子时间线，那么这些子时间线也会停止播放。  当播放的是动画时，<xref:System.Windows.Media.Animation.Timeline.Duration%2A> 属性指定了动画从其起始值转换为结束值所花费的时间。  时间线的持续时间有时称为“简单持续时间”以区分一次迭代的持续时间和动画播放（包括重复）的总时间长度。  您可以使用有限时间值或特殊值（<xref:System.Windows.Duration.Automatic%2A> 或 <xref:System.Windows.Duration.Forever%2A>）指定持续时间。  动画的持续时间应该解析为 <xref:System.Windows.Duration.TimeSpan%2A> 值，这样它就可以在值之间转换。  
  
 下面的示例演示了其 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 属性为 5 秒的 <xref:System.Windows.Media.Animation.DoubleAnimation>。  
  
  
  
 容器时间线（例如 <xref:System.Windows.Media.Animation.Storyboard> 和 <xref:System.Windows.Media.Animation.ParallelTimeline>）的默认持续时间为 <xref:System.Windows.Duration.Automatic%2A>，这意味着当其最后的子时间线停止播放后，它们将自动结束。  下面的示例演示了一个 <xref:System.Windows.Media.Animation.Storyboard>，其 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 解析为 5 秒，这 5 秒是所有其子 <xref:System.Windows.Media.Animation.DoubleAnimation> 对象完成所花费的时间长度。  
  
  
  
 通过将容器时间线的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 设置为 <xref:System.Windows.Duration.TimeSpan%2A> 值，您可以强行使其播放的时间与其子 <xref:System.Windows.Media.Animation.Timeline> 对象播放的时间不同。  如果将 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 设置为一个小于容器时间线的子 <xref:System.Windows.Media.Animation.Timeline> 对象长度的值，那么当容器时间线停止播放时，子 <xref:System.Windows.Media.Animation.Timeline> 对象也会停止播放。  下面的示例将 <xref:System.Windows.Media.Animation.Storyboard> 的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 从前面示例中的值设置为 3 秒。  结果，第一个 <xref:System.Windows.Media.Animation.DoubleAnimation> 将目标矩形宽度动画处理为 60 后，播放了 3 秒就停止播放。  
  
  
  
<a name="repeatinganimations"></a>   
### RepeatBehavior 属性  
 <xref:System.Windows.Media.Animation.Timeline> 控件的 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性控制它重复其简单持续时间的次数。  使用 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性，您可以指定时间线播放的次数（一次迭代 <xref:System.Windows.Media.Animation.RepeatBehavior.Count%2A>）或它将播放的总时间长度（一次重复 <xref:System.Windows.Media.Animation.RepeatBehavior.Duration%2A>）。  无论是哪一种情况，动画都将从头到尾地不断运行许多次，直到完成要求的次数或经历完所需的一段时间。  默认情况下，时间线的迭代次数为 `1.0`，即播放一次时间线，根本不进行重复。  
  
 下面的示例使用 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性指定一个迭代次数来将 <xref:System.Windows.Media.Animation.DoubleAnimation> 播放时间延长为简单持续时间的两倍。  
  
  
  
 接下来的示例使用 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性将 <xref:System.Windows.Media.Animation.DoubleAnimation> 播放时间缩减为简单持续时间的一半。  
  
  
  
 如果将 <xref:System.Windows.Media.Animation.Timeline> 的 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性设置为 <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>，则 <xref:System.Windows.Media.Animation.Timeline> 将会一直重复，直到手动停止或由计时系统停止。  下面的示例使用 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性使 <xref:System.Windows.Media.Animation.DoubleAnimation> 无限次播放。  
  
  
  
 有关其他示例，请参见[重复动画](../../../../docs/framework/wpf/graphics-multimedia/how-to-repeat-an-animation.md)。  
  
<a name="autoreverseproperty"></a>   
### AutoReverse 属性  
 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 属性指定 <xref:System.Windows.Media.Animation.Timeline> 在每次向前迭代结束后是否倒退。  下面的示例将 <xref:System.Windows.Media.Animation.DoubleAnimation> 的 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 属性设置为 `true`，结果，它从 0 到 100 播放动画，然后又从 100 到 0 播放动画。  总共播放了 10 秒。  
  
  
  
 当您使用 <xref:System.Windows.Media.Animation.RepeatBehavior.Count%2A> 值指定 <xref:System.Windows.Media.Animation.Timeline> 的 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>，并且 <xref:System.Windows.Media.Animation.Timeline> 的 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 属性为 `true` 时，一次重复包含一次向前迭代和一次向后迭代。  下面的示例将 <xref:System.Windows.Media.Animation.DoubleAnimation> 的 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 从以前示例中的值设置成 <xref:System.Windows.Media.Animation.RepeatBehavior.Count%2A> 为 2。  结果，<xref:System.Windows.Media.Animation.DoubleAnimation> 播放了 20 秒：向前 5 秒，向后 5 秒，再向前 5 秒，然后再向后 5 秒。  
  
  
  
 如果容器时间线有子 <xref:System.Windows.Media.Animation.Timeline> 对象，当容器时间线反向时，它们也会反向。  有关其他示例，请参见[指定时间线是否自动反转](../../../../docs/framework/wpf/graphics-multimedia/how-to-specify-whether-a-timeline-automatically-reverses.md)。  
  
<a name="timelinebegin"></a>   
## BeginTime 属性  
 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 属性可以让您指定时间线开始的时间。  时间线的开始时间相对于其父时间线。  如果开始时间为 0 秒，则意味着其父时间线开始后，该时间线立即开始；如果设置为其他值，则会在父时间线和子时间线的开始播放时间之间产生一个时间差。  例如，如果开始时间设置为 2 秒，意味着当其父时间线播放 2 秒后，该子时间线才开始播放。  默认情况下，所有时间线的开始时间都为 0 秒。  您也可以将时间线的开始时间设置为 `null`，这会阻止时间线开始播放。  在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，您可以使用 [x:Null 标记扩展](../../../../docs/framework/xaml-services/x-null-markup-extension.md) 指定 Null。  
  
 请注意，每次时间线重复时，因为其 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 设置，不会应用开始时间。  如果您要创建的动画的 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 为 10 秒并且其 <xref:System.Windows.Media.Animation.RepeatBehavior> 为 <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>，则在动画第一次播放前，将会延迟 10 秒，但是后面的每次重复不会这样。  但是，如果动画的父时间线重新开始或重复，则会延迟 10 秒。  
  
 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 属性用于错开时间线。  下面的示例创建一个包含两个子 <xref:System.Windows.Media.Animation.DoubleAnimation> 对象的 <xref:System.Windows.Media.Animation.Storyboard>。  第一个动画的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 为 5 秒，第二个动画的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 为 3 秒。  该示例将第二个 <xref:System.Windows.Media.Animation.DoubleAnimation> 的 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 设置为 5 秒，这样它在第一个 <xref:System.Windows.Media.Animation.DoubleAnimation> 结束后就会开始播放。  
  
  
  
<a name="fillbehaviorproperty"></a>   
## FillBehavior 属性  
 当 <xref:System.Windows.Media.Animation.Timeline> 达到其总活动期的结尾时，<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 属性指定它是停止还是保持其最后的值。  如果动画的 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 为 <xref:System.Windows.Media.Animation.FillBehavior>，则“保持”其输出值：进行动画处理的属性保留动画的最后值。  <xref:System.Windows.Media.Animation.FillBehavior> 值会导致动画在结束后停止影响其目标属性。  
  
 下面的示例创建一个包含两个子 <xref:System.Windows.Media.Animation.DoubleAnimation> 对象的 <xref:System.Windows.Media.Animation.Storyboard>。  两个 <xref:System.Windows.Media.Animation.DoubleAnimation> 对象都将 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.FrameworkElement.Width%2A> 从 0 动画处理到 100。  <xref:System.Windows.Shapes.Rectangle> 元素的未进行动画处理的 <xref:System.Windows.FrameworkElement.Width%2A> 值为 500 个[与设备无关的像素](GTMT)。  
  
-   第一个 <xref:System.Windows.Media.Animation.DoubleAnimation> 的 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 属性设置为默认值 <xref:System.Windows.Media.Animation.FillBehavior>。  结果，矩形的宽度在 <xref:System.Windows.Media.Animation.DoubleAnimation> 结束后保持为 100。  
  
-   第二个 <xref:System.Windows.Media.Animation.DoubleAnimation> 的 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 属性设置为 <xref:System.Windows.Media.Animation.FillBehavior>。  结果，第二个 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.FrameworkElement.Width%2A> 在 <xref:System.Windows.Media.Animation.DoubleAnimation> 结束后还原为 500。  
  
  
  
<a name="speedproperties"></a>   
## 用于控制时间线速度的属性  
 <xref:System.Windows.Media.Animation.Timeline> 类提供三个用于指定其速度的属性：  
  
-   <xref:System.Windows.Media.Animation.Timeline.SpeedRatio%2A> \- 指定 <xref:System.Windows.Media.Animation.Timeline> 相对于其父时间线的时间进度速率。  大于 1 的值增加 <xref:System.Windows.Media.Animation.Timeline> 及其子 <xref:System.Windows.Media.Animation.Timeline> 对象的速率，0 和 1 之间的值减慢其速率。  值 1 表明 <xref:System.Windows.Media.Animation.Timeline> 的进度速率与其父时间线相同。  容器时间线的 <xref:System.Windows.Media.Animation.Timeline.SpeedRatio%2A> 设置也会影响其所有子 <xref:System.Windows.Media.Animation.Timeline> 对象。  
  
-   <xref:System.Windows.Media.Animation.Timeline.AccelerationRatio%2A> \- 指定时间线花费在加速上的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 百分比。  有关示例，请参见[使动画加速或减速](../../../../docs/framework/wpf/graphics-multimedia/how-to-accelerate-or-decelerate-an-animation.md)。  
  
-   <xref:System.Windows.Media.Animation.Timeline.DecelerationRatio%2A> \- 指定时间线花费在减速上的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 百分比。  有关示例，请参见[使动画加速或减速](../../../../docs/framework/wpf/graphics-multimedia/how-to-accelerate-or-decelerate-an-animation.md)。  
  
## 请参阅  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [动画和计时系统概述](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)   
 [计时事件概述](../../../../docs/framework/wpf/graphics-multimedia/timing-events-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)   
 [Animation Timing Behavior Sample](http://go.microsoft.com/fwlink/?LinkID=159970)