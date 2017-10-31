---
title: "如何：为已经到达有效期末尾的时间线指定 FillBehavior | Microsoft Docs"
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
  - "非活动时间线的 FillBehavior 属性"
  - "时间线, FillBehavior 属性"
ms.assetid: db805f59-d513-4dac-af15-47005dae3199
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：为已经到达有效期末尾的时间线指定 FillBehavior
此示例演示如何为动画属性的非活动 <xref:System.Windows.Media.Animation.Timeline> 指定 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>。  
  
## 示例  
 <xref:System.Windows.Media.Animation.Timeline> 的 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 属性决定了在未对动画属性的值进行动画处理时，即在 <xref:System.Windows.Media.Animation.Timeline> 处于非活动状态但其父 <xref:System.Windows.Media.Animation.Timeline> 在其活动或保持期内时，动画属性的值会发生什么情况。  例如，动画结束后动画属性是仍然保留其结束值，还是恢复为动画开始之前所具有的值？  
  
 下面的示例使用 <xref:System.Windows.Media.Animation.DoubleAnimation> 对两个矩形的 <xref:System.Windows.FrameworkElement.Width%2A> 进行动画处理。  每个矩形都使用不同的 <xref:System.Windows.Media.Animation.Timeline> 对象。  
  
 一个 <xref:System.Windows.Media.Animation.Timeline> 具有设置为 <xref:System.Windows.Media.Animation.FillBehavior> 的 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>，因此，在 <xref:System.Windows.Media.Animation.Timeline> 结束时矩形的宽度将恢复为未经过动画处理的值。  另一个 <xref:System.Windows.Media.Animation.Timeline> 具有 <xref:System.Windows.Media.Animation.FillBehavior> 的 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>，因此，在 <xref:System.Windows.Media.Animation.Timeline> 结束时，宽度将保留为其结束值。  
  
 [!code-xml[timingbehaviors_snip#FillBehaviorWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/FillBehaviorExample.xaml#fillbehaviorwholepage)]  
  
 有关完整示例，请参见 [Animation Example Gallery](http://go.microsoft.com/fwlink/?LinkID=159969)（动画示例库）。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.DoubleAnimation>   
 <xref:System.Windows.FrameworkElement.Width%2A>   
 <xref:System.Windows.Media.Animation.Timeline>   
 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>   
 <xref:System.Windows.Media.Animation.FillBehavior>   
 <xref:System.Windows.Media.Animation.FillBehavior>   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Animation and Timing](http://msdn.microsoft.com/zh-cn/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)