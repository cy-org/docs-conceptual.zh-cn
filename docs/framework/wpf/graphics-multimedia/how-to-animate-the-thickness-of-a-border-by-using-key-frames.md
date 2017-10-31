---
title: "如何：使用关键帧对边框的粗细进行动画处理 | Microsoft Docs"
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
  - "动画, 使用关键帧对边框的粗细进行动画处理"
  - "边框粗细, 使用关键帧进行动画处理"
  - "关键帧, 对边框的粗细进行动画处理"
ms.assetid: 3a9cb463-0a63-407d-aae7-3fbb1a559947
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用关键帧对边框的粗细进行动画处理
此示例演示如何对 <xref:System.Windows.Controls.Border> 的 <xref:System.Windows.Controls.Control.BorderThickness%2A> 属性进行动画处理。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.Animation.ThicknessAnimationUsingKeyFrames> 类对 <xref:System.Windows.Controls.Border> 的 <xref:System.Windows.Controls.Control.BorderThickness%2A> 属性进行动画处理。  此动画按下列方式使用三个关键帧：  
  
1.  在最初的半秒内，将使用 <xref:System.Windows.Media.Animation.LinearThicknessKeyFrame> 类的实例逐渐增加边框的粗细。  此示例使用 <xref:System.Windows.Media.Animation.LinearThicknessKeyFrame> 在值之间创建平滑的线性递增。  
  
2.  在接下来的半秒结束时，将使用 <xref:System.Windows.Media.Animation.DiscreteThicknessKeyFrame> 类的实例突然增加边框的粗细。  离散关键帧（如从 <xref:System.Windows.Media.Animation.DiscreteThicknessKeyFrame> 派生的那些关键帧）将在值之间创建突然跳转，使动画出现跳帧效果。  
  
3.  在最后两秒内，将使用 <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame> 类的实例减小边框的粗细。  [样条](GTMT)关键帧与从 <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame> 派生的关键帧一样，根据 <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame.KeySpline%2A> 属性的值在各个值之间创建可变过渡。  在此关键帧中，动画一开始较慢，然后以指数级加速，直至时间段结束。  
  
 [!code-xml[keyframes_snip#ThicknessAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ThicknessAnimationUsingKeyFramesExample.xaml#thicknessanimationusingkeyframeswholepage)]  
  
 有关完整示例，请参见 [KeyFrame Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160012)（KeyFrame 动画示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.LinearThicknessKeyFrame>   
 <xref:System.Windows.Media.Animation.DiscreteThicknessKeyFrame>   
 <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame>   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [关键帧动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)   
 [对 BorderThickness 值进行动画处理](../../../../docs/framework/wpf/controls/how-to-animate-a-borderthickness-value.md)