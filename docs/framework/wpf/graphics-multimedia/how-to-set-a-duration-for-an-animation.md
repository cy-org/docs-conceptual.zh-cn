---
title: "如何：设置动画的持续时间 | Microsoft Docs"
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
  - "动画, duration"
  - "动画的持续时间"
  - "时间线, description"
ms.assetid: 155034ef-7d00-4416-a73c-b1713992d2eb
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：设置动画的持续时间
<xref:System.Windows.Media.Animation.Timeline> 表示时间段，该时间段的长度由时间线的 <xref:System.Windows.Duration> 确定。  当 <xref:System.Windows.Media.Animation.Timeline> 达到其持续时间的终点时，就会停止播放。  如果该 <xref:System.Windows.Media.Animation.Timeline> 具有子时间线，那么这些子时间线也会停止播放。  当播放的是动画时，<xref:System.Windows.Duration> 指定了动画从其起始值转换为结束值所花费的时间。  
  
 您可以使用特定有限时间值或特殊值（<xref:System.Windows.Duration.Automatic%2A> 或 <xref:System.Windows.Duration.Forever%2A>）指定 <xref:System.Windows.Duration>。  动画的持续时间必须始终为时间值，因为动画必须始终有一个已定义的有限长度，否则动画不知道如何在其目标值之间转换。  容器时间线（<xref:System.Windows.Media.Animation.TimelineGroup> 对象，例如 <xref:System.Windows.Media.Animation.Storyboard> 和 <xref:System.Windows.Media.Animation.ParallelTimeline>）的默认持续时间为 <xref:System.Windows.Duration.Automatic%2A>，这意味着当其最后的子时间线停止播放后，它们将自动结束。  
  
 下面的示例演示如何对 <xref:System.Windows.Shapes.Rectangle> 的宽度、高度和填充色进行动画处理。  持续时间是在动画和产生动画效果容器时间线上设置的，包括控制动画的感觉速度和用容器时间线持续时间重写子时间线持续时间。  
  
## 示例  
 [!code-xml[timingbehaviors_snip#DurationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/DurationExample.xaml#durationexamplewholepage)]  
  
## 请参阅  
 <xref:System.Windows.Duration>   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)