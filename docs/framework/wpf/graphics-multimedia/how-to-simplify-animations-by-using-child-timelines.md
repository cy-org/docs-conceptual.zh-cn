---
title: "如何：使用子时间线简化动画 | Microsoft Docs"
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
  - "动画, 通过子时间线简化"
  - "子时间线"
  - "通过子时间线简化动画"
ms.assetid: 8335d770-d13d-42bd-8dfa-63f92c0327e2
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：使用子时间线简化动画
此示例演示如何使用子 <xref:System.Windows.Media.Animation.ParallelTimeline> 对象简化动画。  <xref:System.Windows.Media.Animation.Storyboard> 是一种为其包含的时间线提供目标信息的 <xref:System.Windows.Media.Animation.Timeline>。  使用 <xref:System.Windows.Media.Animation.Storyboard> 来提供时间线目标信息，其中包括对象和属性信息。  
  
 若要开始动画，请使用一个或多个 <xref:System.Windows.Media.Animation.ParallelTimeline> 对象作为 <xref:System.Windows.Media.Animation.Storyboard> 的嵌套子元素。  这些 <xref:System.Windows.Media.Animation.ParallelTimeline> 对象可以包含其他动画，因此可以更好地封装复杂动画中的计时序列。  例如，如果要使同一 <xref:System.Windows.Media.Animation.Storyboard> 中的 <xref:System.Windows.Controls.TextBlock> 和若干形状产生动画效果，您可以将 <xref:System.Windows.Controls.TextBlock> 和形状的动画分开，将每个动画分别放在单独的 <xref:System.Windows.Media.Animation.ParallelTimeline> 中。  由于每个 <xref:System.Windows.Media.Animation.ParallelTimeline> 都有自己的 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A>，并且 <xref:System.Windows.Media.Animation.ParallelTimeline> 的所有子元素都相对于此 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 开始，因此可以更好地封装计时。  
  
 下面的示例使同一 <xref:System.Windows.Media.Animation.Storyboard> 内的两段文本（<xref:System.Windows.Controls.TextBlock> 对象）产生动画效果。  <xref:System.Windows.Media.Animation.ParallelTimeline> 封装其中一个 <xref:System.Windows.Controls.TextBlock> 对象的动画。  
  
 **性能说明：**尽管可以将 <xref:System.Windows.Media.Animation.Storyboard> 时间线相互嵌套，但 <xref:System.Windows.Media.Animation.ParallelTimeline> 更适合于嵌套，因为它们需要的系统开销较少。  （<xref:System.Windows.Media.Animation.Storyboard> 类从 <xref:System.Windows.Media.Animation.ParallelTimeline> 类继承。）  
  
## 示例  
 [!code-xml[Timelines_snip#ParallelTimelineWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Timelines_snip/CS/ParallelTimelineExample.xaml#paralleltimelinewholepage)]  
  
## 请参阅  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [指定演示图板动画之间的 HandoffBehavior](../../../../docs/framework/wpf/graphics-multimedia/how-to-specify-handoffbehavior-between-storyboard-animations.md)