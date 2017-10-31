---
title: "如何：重复动画 | Microsoft Docs"
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
  - "动画, 重复"
  - "时间线的 RepeatBehavior 属性"
  - "重复动画"
  - "时间线 RepeatBehavior 属性"
ms.assetid: e6f3b068-eeeb-47fd-8d40-8848c31f1e1e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：重复动画
此示例演示如何使用 <xref:System.Windows.Media.Animation.Timeline> 的 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性控制动画的重复行为。  
  
## 示例  
 <xref:System.Windows.Media.Animation.Timeline> 的 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性控制动画重复其简单期间的次数。  通过使用 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>，您可以指定让 <xref:System.Windows.Media.Animation.Timeline> 重复一定的次数（重复次数）或在指定的一段时间内发生重复。  无论是哪一种情况，动画都将从头到尾地不断运行，直到完成要求的次数或经历完所需的一段时间。  
  
 默认情况下，时间线的重复次数为 1.0，即播放一次时间线，不进行重复。  但是，如果将 <xref:System.Windows.Media.Animation.Timeline> 的 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性设置为 <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>，则时间线将会无限重复。  
  
 下面的示例演示如何使用 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性控制动画的重复行为。  此示例对五个矩形的 <xref:System.Windows.FrameworkElement.Width%2A> 属性进行动画处理，每个矩形使用了不同类型的重复行为。  
  
 [!code-xml[timingbehaviors_snip#RepeatBehaviorWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/RepeatBehaviorExample.xaml#repeatbehaviorwholepage)]  
  
 有关完整示例，请参见 [Animation Timing Behavior Sample](http://go.microsoft.com/fwlink/?LinkID=159970)（动画计时行为示例）。  
  
## 请参阅  
 [在重复循环过程中累积动画值](../../../../docs/framework/wpf/graphics-multimedia/how-to-accumulate-animation-values-during-repeat-cycles.md)   
 [指定时间线是否自动反转](../../../../docs/framework/wpf/graphics-multimedia/how-to-specify-whether-a-timeline-automatically-reverses.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)   
 [Animation and Timing](http://msdn.microsoft.com/zh-cn/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Animation Timing Behavior Sample](http://go.microsoft.com/fwlink/?LinkID=159970)