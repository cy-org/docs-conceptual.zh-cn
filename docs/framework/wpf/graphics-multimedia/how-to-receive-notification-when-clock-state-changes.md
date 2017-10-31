---
title: "如何：在时钟状态发生变化时接收通知 | Microsoft Docs"
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
  - "时钟, 状态更改通知"
  - "通知, 时钟的状态更改"
ms.assetid: ecb10fc9-d0c2-45c3-b0a1-7b11baa733da
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：在时钟状态发生变化时接收通知
当时钟的 <xref:System.Windows.Media.Animation.Clock.CurrentState%2A> 变为无效时（例如时钟启动或停止时），将发生该时钟的 <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> 事件。  您可以直接使用 <xref:System.Windows.Media.Animation.Clock> 注册此事件，也可以使用 <xref:System.Windows.Media.Animation.Timeline> 注册。  
  
 在下面的示例中，<xref:System.Windows.Media.Animation.Storyboard> 和两个 <xref:System.Windows.Media.Animation.DoubleAnimation> 对象用于对两个矩形的宽度进行动画处理。  <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> 事件用于侦听时钟状态变化。  
  
## 示例  
 [!code-xml[timingbehaviors_snip#_graphicsmm_StateExampleMarkupWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StateExample.xaml#_graphicsmm_stateexamplemarkupwholepage)]  
  
 [!code-csharp[timingbehaviors_snip#_graphicsmm_StateEventHandlers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StateExample.xaml.cs#_graphicsmm_stateeventhandlers)]
 [!code-vb[timingbehaviors_snip#_graphicsmm_StateEventHandlers](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/stateexample.xaml.vb#_graphicsmm_stateeventhandlers)]  
  
 下图显示了随着父时间线（*演示图板*）的延伸，动画所进入的不同状态。  
  
 ![具有两个动画的演示图板的时钟状态](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-3timelines.png "graphicsmm\_3timelines")  
  
 下表显示了激发 *Animation1* 的 <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> 事件的时间：  
  
||||||||  
|-|-|-|-|-|-|-|  
|时间（秒）|1|10|19|21|30|39|  
|省\/市\/自治区|活动|活动|Stopped|活动|活动|Stopped|  
  
 下表显示了激发 *Animation2* 的 <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> 事件的时间：  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
|时间（秒）|1|9|11|19|21|29|31|39|  
|省\/市\/自治区|活动|Filling|活动|Stopped|活动|Filling|活动|Stopped|  
  
 请注意，*Animation1* 的 <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> 事件在第 10 秒时激发，尽管其状态仍保持为 <xref:System.Windows.Media.Animation.ClockState>。  这是因为其状态在第 10 秒时发生变化，但状态从 <xref:System.Windows.Media.Animation.ClockState> 变化为 <xref:System.Windows.Media.Animation.ClockState>，然后在同一瞬间又变回 <xref:System.Windows.Media.Animation.ClockState>。