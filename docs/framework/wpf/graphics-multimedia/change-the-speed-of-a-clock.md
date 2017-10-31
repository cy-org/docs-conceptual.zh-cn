---
title: "如何：在不更改时间线速度的情况下更改时钟速度 | Microsoft Docs"
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
  - "时钟, 更改速度"
  - "时钟速度, 更改"
ms.assetid: 72f36dd0-f085-445d-8589-19a83fe74f5e
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：在不更改时间线速度的情况下更改时钟速度
使用 <xref:System.Windows.Media.Animation.ClockController> 对象的 <xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A> 属性，可以在不改变时钟的 <xref:System.Windows.Media.Animation.Timeline> 的 <xref:System.Windows.Media.Animation.Timeline.SpeedRatio%2A> 的情况下，更改 <xref:System.Windows.Media.Animation.Clock> 的速度。  在下面的示例中，<xref:System.Windows.Media.Animation.ClockController> 用于以交互方式修改时钟的 <xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A>。  <xref:System.Windows.Media.Animation.Clock.CurrentGlobalSpeedInvalidated> 事件以及时钟的 <xref:System.Windows.Media.Animation.Clock.CurrentGlobalSpeed%2A> 属性用于在每次更改时钟的交互式 <xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A> 时显示时钟的当前全局速度。  
  
## 示例  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMClockControllerSpeedRatioExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/ClockControllerSpeedRatioExample.cs#graphicsmmclockcontrollerspeedratioexample)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMClockControllerSpeedRatioExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/clockcontrollerspeedratioexample.vb#graphicsmmclockcontrollerspeedratioexample)]