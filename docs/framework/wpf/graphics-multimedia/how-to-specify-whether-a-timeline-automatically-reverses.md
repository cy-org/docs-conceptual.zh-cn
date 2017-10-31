---
title: "如何：指定时间线是否自动反转 | Microsoft Docs"
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
  - "时间线的 AutoReverse 属性"
  - "时间线, AutoReverse 属性"
ms.assetid: 1648dd90-1bee-409a-ac69-ac729867f557
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：指定时间线是否自动反转
时间线的 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 属性确定它在完成前向迭代之后是否反向播放。  下面的示例演示了几个具有相同持续时间和目标值但是具有不同 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 设置的动画。  为了演示 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 属性在不同 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 设置下的行为，可以将某些动画设置为重复播放。  最后一个动画演示了 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 属性如何在嵌套时间线上工作。  
  
## 示例  
 [!code-xml[timingbehaviors_snip#AutoReverseAndRepeatBehaviorExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AutoReverseExample.xaml#autoreverseandrepeatbehaviorexamplewholepage)]