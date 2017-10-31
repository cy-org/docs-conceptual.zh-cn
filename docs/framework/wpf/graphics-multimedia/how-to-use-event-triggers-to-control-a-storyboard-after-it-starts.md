---
title: "如何：在演示图板启动之后使用事件触发器来控制演示图板 | Microsoft Docs"
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
  - "事件触发器, 控制演示图板"
  - "情节提要, 启动后控制"
  - "触发器, 控制演示图板"
ms.assetid: 3b115594-6a93-4972-b24d-61aa16f1c15f
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：在演示图板启动之后使用事件触发器来控制演示图板
此示例演示如何在 <xref:System.Windows.Media.Animation.Storyboard> 启动后对它进行控制。  若要使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 启动 <xref:System.Windows.Media.Animation.Storyboard>，请使用 <xref:System.Windows.Media.Animation.BeginStoryboard>，它可以将动画分发到要进行动画处理的对象和属性，然后启动 Storyboard。  如果通过指定 <xref:System.Windows.Media.Animation.BeginStoryboard> 的 <xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A> 属性为它提供一个名称，则它将成为可控制的 Storyboard。  然后，可以在 Storyboard 启动后以交互方式对它进行控制。  
  
 将以下 Storyboard 操作与 <xref:System.Windows.EventTrigger> 对象一起使用可以控制 Storyboard。  
  
-   <xref:System.Windows.Media.Animation.PauseStoryboard>：暂停 Storyboard。  
  
-   <xref:System.Windows.Media.Animation.ResumeStoryboard>：继续暂停的 Storyboard。  
  
-   <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>：更改 Storyboard 速度。  
  
-   <xref:System.Windows.Media.Animation.SkipStoryboardToFill>：使 Storyboard 前进到其填充期的末尾（如果有填充期）。  
  
-   <xref:System.Windows.Media.Animation.StopStoryboard>：停止 Storyboard。  
  
-   <xref:System.Windows.Media.Animation.RemoveStoryboard>：移除 Storyboard，释放资源。  
  
## 示例  
 下面的示例使用可控制的 Storyboard 操作来以交互方式控制 Storyboard。  
  
 **注意：**若要查看使用代码控制 Storyboard 的示例，请参见[在演示图板启动后使用其交互式方法对其进行控制](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-storyboard-after-it-starts.md)。  
  
 [!code-xml[timingbehaviors_snip#ControlStoryboardExampleUsingWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/ControlStoryboardExample.xaml#controlstoryboardexampleusingwholepage)]  
  
 有关其他示例，请参见 [Animation Example Gallery](http://go.microsoft.com/fwlink/?LinkID=159969)（动画示例库）。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.ResumeStoryboard>   
 <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>   
 <xref:System.Windows.Media.Animation.SkipStoryboardToFill>   
 <xref:System.Windows.Media.Animation.PauseStoryboard>   
 <xref:System.Windows.Media.Animation.StopStoryboard>   
 <xref:System.Windows.Media.Animation.SeekStoryboard>   
 [在演示图板启动后使用其交互式方法对其进行控制](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-storyboard-after-it-starts.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)