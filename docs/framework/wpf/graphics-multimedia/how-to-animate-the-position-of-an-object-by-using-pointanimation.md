---
title: "如何：使用 PointAnimation 针对对象的位置进行动画处理 | Microsoft Docs"
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
  - "动画, PointAnimation"
  - "类, PointAnimation"
  - "图形 [WPF], 动画"
  - "PointAnimation 类"
ms.assetid: 42310977-cc90-438a-8a47-0345898e01be
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使用 PointAnimation 针对对象的位置进行动画处理
此示例演示如何使用 <xref:System.Windows.Media.Animation.PointAnimation> 类，使对象沿着某个<xref:System.Windows.Shapes.Path>进行动画显示。  
  
## 示例  
 下面的示例使一个椭圆沿着某个<xref:System.Windows.Shapes.Path>从屏幕上的一个点移到另一个点。  该示例使用 <xref:System.Windows.Media.Animation.PointAnimation> 对 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 属性进行动画处理，从而对 <xref:System.Windows.Media.EllipseGeometry> 的位置进行动画处理。  
  
 [!code-csharp[BasicAnimations_snip#PointAnimationWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snip/CSharp/PointAnimationExample.cs#pointanimationwholepage)]
 [!code-vb[BasicAnimations_snip#PointAnimationWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BasicAnimations_snip/VisualBasic/PointAnimationExample.vb#pointanimationwholepage)]  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.PointAnimation>   
 <xref:System.Windows.Shapes.Path>   
 <xref:System.Windows.Media.EllipseGeometry>   
 <xref:System.Windows.Media.EllipseGeometry.Center%2A>   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [图形和多媒体](../../../../docs/framework/wpf/graphics-multimedia/index.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/graphics-how-to-topics.md)   
 [Animation and Timing](http://msdn.microsoft.com/zh-cn/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)