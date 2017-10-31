---
title: "如何：控制关键帧动画的计时 | Microsoft Docs"
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
  - "关键帧 [WPF], 计时"
  - "对关键帧动画进行计时"
ms.assetid: b059216f-7d4b-4ca8-a019-bc287ee7bf16
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：控制关键帧动画的计时
此示例演示如何在关键帧动画内控制关键帧的计时。  像其他动画一样，关键帧动画具有 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 属性。  除了指定动画的持续时间外，您还需要指定为动画的各个关键帧分配持续时间内的一段多长时间。  若要分配时间，请为动画中的每个关键帧指定 <xref:System.Windows.Media.Animation.KeyTime>。  
  
 每个关键帧的 <xref:System.Windows.Media.Animation.KeyTime> 指定关键帧在何时结束（它未指定关键帧播放的时间长度）。  您可以采用以下形式指定 <xref:System.Windows.Media.Animation.KeyTime>：<xref:System.TimeSpan> 值、百分比或者 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> 或 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> 特殊值。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 对横跨屏幕的矩形进行动画处理。  关键帧的关键时间是用 <xref:System.TimeSpan> 值设置的。  
  
 [!code-csharp[keyframes_snip#KeyTimesTimeSpanExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimestimespanexample)]
 [!code-vb[keyframes_snip#KeyTimesTimeSpanExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimestimespanexample)]
 [!code-xml[keyframes_snip#KeyTimesTimeSpanExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimestimespanexample)]  
  
 下图显示达到每个关键帧的值的时间。  
  
 ![在 3、4 和 10 秒时达到的关键值](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-keyframe-keytime1-timespan.png "graphicsmm\_keyframe\_keytime1\_timespan")  
  
 下一示例演示一个相同的动画，只是关键帧的关键时间是用百分比值设置的。  
  
 [!code-csharp[keyframes_snip#KeyTimesPercentageExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimespercentageexample)]
 [!code-vb[keyframes_snip#KeyTimesPercentageExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimespercentageexample)]
 [!code-xml[keyframes_snip#KeyTimesPercentageExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimespercentageexample)]  
  
 下图显示达到每个关键帧的值的时间。  
  
 ![在 3、4 和 10 秒时达到的关键值](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-keyframe-keytime2-percentage.png "graphicsmm\_keyframe\_keytime2\_percentage")  
  
 下一示例使用 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> 关键时间值。  
  
 [!code-csharp[keyframes_snip#KeyTimesUniformExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimesuniformexample)]
 [!code-vb[keyframes_snip#KeyTimesUniformExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimesuniformexample)]
 [!code-xml[keyframes_snip#KeyTimesUniformExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimesuniformexample)]  
  
 下图显示达到每个关键帧的值的时间。  
  
 ![在 3.3、6.6 和 9.9 秒时达到的关键值](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-keyframe-keytime3-uniform.png "graphicsmm\_keyframe\_keytime3\_uniform")  
  
 最后一个示例使用 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> 关键时间值。  
  
 [!code-csharp[keyframes_snip#KeyTimesPacedExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimespacedexample)]
 [!code-vb[keyframes_snip#KeyTimesPacedExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimespacedexample)]
 [!code-xml[keyframes_snip#KeyTimesPacedExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimespacedexample)]  
  
 下图显示达到每个关键帧的值的时间。  
  
 ![在 0、5 和 10 秒时达到的关键值](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-keyframe-keytime4-paced.png "graphicsmm\_keyframe\_keytime4\_paced")  
  
 为了简单起见，此示例的代码版本使用本地动画（而不是演示图板），原因是只会将单一动画应用于单一属性，但您可以修改示例以改用演示图板。  有关演示如何在代码中声明演示图板的示例，请参见[使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)。  
  
 有关完整示例，请参见 [KeyFrame Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160012)（KeyFrame 动画示例）。  有关关键帧动画的更多信息，请参见[关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)。  
  
## 请参阅  
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)