---
title: "如何：对 BorderThickness 值进行动画处理 | Microsoft Docs"
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
  - "动画, 对边框粗细的更改"
  - "边框粗细, 对更改进行动画处理"
ms.assetid: fd021978-f74b-4e7b-a7f7-3987dcad9e0f
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：对 BorderThickness 值进行动画处理
此示例演示如何使用 <xref:System.Windows.Media.Animation.ThicknessAnimation> 类对边框粗细的更改进行动画处理。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.Animation.ThicknessAnimation> 对边框的粗细进行动画处理。  此示例使用 <xref:System.Windows.Controls.Border> 的 <xref:System.Windows.Controls.Border.BorderThickness%2A> 属性。  
  
 [!code-csharp[BasicAnimations_snip#ThicknessAnimationWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snip/CSharp/ThicknessAnimationExample.cs#thicknessanimationwholepage)]
 [!code-vb[BasicAnimations_snip#ThicknessAnimationWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BasicAnimations_snip/VisualBasic/ThicknessAnimationExample.vb#thicknessanimationwholepage)]  
  
 有关完整示例，请参见 [Animation Example Gallery](http://go.microsoft.com/fwlink/?LinkID=159969)（动画示例库）。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.ThicknessAnimation>   
 <xref:System.Windows.Controls.Border.BorderThickness%2A>   
 <xref:System.Windows.Controls.Border>   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Animation and Timing](http://msdn.microsoft.com/zh-cn/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)   
 [使用关键帧对边框的粗细进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-the-thickness-of-a-border-by-using-key-frames.md)