---
title: "如何：指定演示图板动画之间的 HandoffBehavior | Microsoft Docs"
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
  - "动画, 之间的切换行为"
  - "情节提要, 动画之间的切换行为"
ms.assetid: 97bd6842-929b-49d9-813e-46553ae46472
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：指定演示图板动画之间的 HandoffBehavior
本示例演示如何指定演示图板动画之间的切换行为。  <xref:System.Windows.Media.Animation.BeginStoryboard> 的 <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A> 属性指定新动画如何与已经应用于属性的任何现有动画交互。  
  
## 示例  
 下面的示例创建两个按钮，当鼠标光标移到这两个按钮上时，它们将变大，当鼠标光标移开时，它们将变小。  如果将鼠标移到一个按钮上然后快速移走光标，则在第一个动画完成之前将应用第二个动画。  当两个动画像这样重叠时，您可以看到 <xref:System.Windows.Media.Animation.HandoffBehavior> 和 <xref:System.Windows.Media.Animation.HandoffBehavior> 的 <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A> 值之间存在差异。  如果值为 <xref:System.Windows.Media.Animation.HandoffBehavior>，在出现动画重叠时，动画之间的过渡将较为平滑，而如果值为 <xref:System.Windows.Media.Animation.HandoffBehavior>，则会使新动画立即取代之前的重叠动画。  
  
 [!code-xml[timingbehaviors_snip#HandoffBehaviorWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/HandoffBehaviorExample.xaml#handoffbehaviorwholepage)]  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.BeginStoryboard>   
 <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A>   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Animation and Timing](http://msdn.microsoft.com/zh-cn/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)