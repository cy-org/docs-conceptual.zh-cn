---
title: "如何：使用关键帧对字符串进行动画处理 | Microsoft Docs"
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
  - "动画, 使用关键帧对字符串进行动画处理"
  - "关键帧, 对字符串进行动画处理"
  - "字符串, 使用关键帧进行动画处理"
ms.assetid: c62bc9fd-c09a-4227-bce0-0a1ab82049dd
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用关键帧对字符串进行动画处理
此示例演示如何使用关键帧对字符串（本例中为 <xref:System.Windows.Controls.Button> 控件的 <xref:System.Windows.Controls.ContentControl.Content%2A> 属性）进行动画处理。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames> 类对 <xref:System.Windows.Controls.Button> 的 <xref:System.Windows.Controls.ContentControl.Content%2A> 属性进行动画处理。  
  
 此示例中的所有关键帧均使用 <xref:System.Windows.Media.Animation.DiscreteStringKeyFrame> 类的实例，因为用关键帧创建的字符串动画只能使用离散关键帧。  离散关键帧（如 <xref:System.Windows.Media.Animation.DiscreteStringKeyFrame>）将使值发生突变，也就是说，动画变化是快速发生的，并且不是细微变化。  
  
 [!code-xml[keyframes_snip#StringAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/StringAnimationUsingKeyFramesExample.xaml#stringanimationusingkeyframeswholepage)]  
  
 有关完整示例，请参见 [KeyFrame Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160012)（KeyFrame 动画示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>   
 <xref:System.Windows.Controls.ContentControl.Content%2A>   
 <xref:System.Windows.Controls.Button>   
 <xref:System.Windows.Media.Animation.DiscreteStringKeyFrame>   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [关键帧动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)