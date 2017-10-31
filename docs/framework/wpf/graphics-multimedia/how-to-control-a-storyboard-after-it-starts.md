---
title: "如何：在演示图板启动后对其进行控制 | Microsoft Docs"
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
  - "情节提要, 启动后控制"
ms.assetid: 040f13f0-69f9-4ab5-be2b-079f4f80c7c0
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：在演示图板启动后对其进行控制
本示例演示如何使用代码在 <xref:System.Windows.Media.Animation.Storyboard> 启动后对其进行控制。  若要通过 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 控制演示图板，请使用 <xref:System.Windows.Trigger> 和 <xref:System.Windows.TriggerAction> 对象；有关示例，请参见[在演示图板启动之后使用事件触发器来控制演示图板](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)。  
  
 若要启动演示图板，应使用它的 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法，此方法将演示图板的动画分发给要进行动画处理的属性，然后启动演示图板。  
  
 若要使演示图板可控制，应使用 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法并指定 **true** 作为第二个参数。  然后可以使用演示图板的交互式方法来暂停、继续、搜寻、停止、加速或减慢演示图板，或者使它前进到填充期。  下面列出了演示图板的交互式方法：  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Pause%2A>：暂停演示图板。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Resume%2A>：继续暂停的演示图板。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.SetSpeedRatio%2A>：设置演示图板的交互速度。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>：搜寻到指定的演示图板位置。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.SeekAlignedToLastTick%2A>：搜寻到指定的演示图板位置。  与 <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> 方法不同，此操作是在下一计时周期之前处理的。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.SkipToFill%2A>：使演示图板前进到其填充期（如果有填充期）。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Stop%2A>：停止演示图板。  
  
 在下面的示例中，使用了几个演示图板方法来以交互方式控制演示图板。  
  
 **注意：**若要查看通过 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 使用触发器控制演示图板的示例，请参见[在演示图板启动之后使用事件触发器来控制演示图板](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)。  
  
## 示例  
 [!code-csharp[timingbehaviors_procedural_snip#ControlStoryboardExampleUsingWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/ControlStoryboardExample.cs#controlstoryboardexampleusingwholepage)]
 [!code-vb[timingbehaviors_procedural_snip#ControlStoryboardExampleUsingWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/controlstoryboardexample.vb#controlstoryboardexampleusingwholepage)]  
  
## 请参阅  
 [在演示图板启动之后使用事件触发器来控制演示图板](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)