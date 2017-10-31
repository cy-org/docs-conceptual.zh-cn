---
title: "如何：使用关键帧对大小变化进行动画处理 | Microsoft Docs"
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
  - "动画, 使用关键帧对大小更改进行动画处理"
  - "关键帧, 对大小更改进行动画处理"
  - "大小更改, 使用关键帧进行动画处理"
ms.assetid: 86bd2950-d4c9-4ec4-aa8d-7dc3ccadded4
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用关键帧对大小变化进行动画处理
此示例演示如何使用关键帧对大小变化进行动画处理。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.Animation.SizeAnimationUsingKeyFrames> 类对 <xref:System.Windows.Media.ArcSegment> 的 <xref:System.Windows.Media.ArcSegment.Size%2A> 属性进行动画处理。  此动画按下列方式使用三个关键帧：  
  
1.  在动画的前半秒中，使用 <xref:System.Windows.Media.Animation.LinearSizeKeyFrame> 类的实例逐渐增加弧的大小。  诸如 <xref:System.Windows.Media.Animation.LinearSizeKeyFrame> 的线性关键帧在值之间创建平滑的线性过渡。  
  
2.  在接下来的半秒结束时，使用 <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame> 类的实例突然增加弧的大小。  离散关键帧（如 <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame>）将使值发生突变，也就是说，大小变化是突然发生的，并且不是细微变化。  
  
3.  在最后两秒钟内，使用 <xref:System.Windows.Media.Animation.SplineSizeKeyFrame> 类的实例增加弧的大小。  [样条](GTMT)关键帧（如 <xref:System.Windows.Media.Animation.SplineSizeKeyFrame>）将会根据 <xref:System.Windows.Media.Animation.SplineSizeKeyFrame.KeySpline%2A> 属性的值在各个值之间创建可变过渡。  在本例中，弧的大小首先慢慢增加，然后呈指数方式增加直至时间段结束。  
  
 [!code-xml[keyframes_snip#SizeAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/SizeAnimationUsingKeyFramesExample.xaml#sizeanimationusingkeyframeswholepage)]  
  
 有关完整示例，请参见 [KeyFrame Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160012)（KeyFrame 动画示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.SizeAnimationUsingKeyFrames>   
 <xref:System.Windows.Media.ArcSegment.Size%2A>   
 <xref:System.Windows.Media.ArcSegment>   
 <xref:System.Windows.Media.Animation.LinearSizeKeyFrame>   
 <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame>   
 <xref:System.Windows.Media.Animation.SplineSizeKeyFrame>   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [关键帧动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)