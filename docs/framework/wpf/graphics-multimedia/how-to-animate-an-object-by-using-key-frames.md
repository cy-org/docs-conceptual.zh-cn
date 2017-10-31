---
title: "如何：使用关键帧针对对象进行动画处理 | Microsoft Docs"
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
  - "动画, 使用关键帧对对象进行动画处理"
  - "关键帧, 对对象进行动画处理"
ms.assetid: b1f15ba9-cac7-4cea-8699-5c6b55c05c5e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用关键帧针对对象进行动画处理
此示例演示如何使用关键帧对对象（本例中为 <xref:System.Windows.Controls.Page> 控件的 <xref:System.Windows.Controls.Page.Background%2A> 属性）进行动画处理。  
  
## 示例  
 下面示例使用 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> 类对 <xref:System.Windows.Controls.Page> 控件的 <xref:System.Windows.Controls.Page.Background%2A> 属性的颜色变化进行动画处理。  该示例动画将按固定时间间隔变为不同的背景画笔。  此动画使用 <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> 类创建三个不同的关键帧。  动画按下列方式使用关键帧：  
  
1.  在第一秒结束时，对 <xref:System.Windows.Media.LinearGradientBrush> 类的实例进行动画处理。  示例的此部分将线性渐变应用于背景颜色，使颜色从黄色过渡到橙色再过渡到红色。  
  
2.  在下一秒结束时，对 <xref:System.Windows.Media.RadialGradientBrush> 类的实例进行动画处理。  示例的此部分将径向渐变应用于背景颜色，使颜色从白色过渡到蓝色再过渡到黑色。  
  
3.  在第三秒结束时，对 <xref:System.Windows.Media.DrawingBrush> 类的实例进行动画处理。  示例的此部分将棋盘图案应用于背景。  
  
4.  动画将再次开始并无限重复。  
  
> [!NOTE]
>  <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> 是唯一可与 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> 类一起使用的关键帧类型。  像 <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> 这样的关键帧会使值突然发生更改，也就是说，此示例中的颜色会突然发生变化。  
  
 [!code-xml[keyframes_snip#ObjectAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ObjectAnimationUsingKeyFramesExample.xaml#objectanimationusingkeyframeswholepage)]  
  
 有关完整示例，请参见 [KeyFrame Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160012)（KeyFrame 动画示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>   
 <xref:System.Windows.Controls.Page.Background%2A>   
 <xref:System.Windows.Controls.Page>   
 <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame>   
 <xref:System.Windows.Media.LinearGradientBrush>   
 <xref:System.Windows.Media.RadialGradientBrush>   
 <xref:System.Windows.Media.DrawingBrush>   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [关键帧动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)