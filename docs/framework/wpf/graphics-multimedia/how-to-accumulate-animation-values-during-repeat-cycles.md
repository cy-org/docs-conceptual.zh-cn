---
title: "如何：在重复循环过程中累积动画值 | Microsoft Docs"
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
  - "通过重复循环累积动画值"
  - "动画, 通过重复循环累积值"
ms.assetid: 548df369-c7cc-4dab-b569-08b95ced2e7e
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：在重复循环过程中累积动画值
本示例演示如何使用 <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> 属性在重复过程中累积动画值。  
  
## 示例  
 使用 <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> 属性可在重复过程中累积动画的基值。  例如，如果将动画设置为重复 9 次 \(<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> \= "9x"\)，并将该属性设置为在 10 和 15 之间进行动画移动（From \= 10，To \= 15），则该属性在第一个过程中从 10 移动到 15，在第二个过程中从 15 移动到 20，在第三个过程中从 20 移动到 25，依此类推。  因此，每个动画过程都使用上一动画过程中的动画结束值作为其基值。  
  
 您可以将 `IsCumulative` 属性用于大多数基本动画和大多数关键帧动画。  有关更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)和[关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)。  
  
 下面的示例通过对四个矩形的宽度进行动画处理来演示此行为。  该示例可实现如下功能：  
  
-   使用 <xref:System.Windows.Media.Animation.DoubleAnimation> 对第一个矩形进行动画处理，并将 <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> 属性设置为 `true`。  
  
-   使用 <xref:System.Windows.Media.Animation.DoubleAnimation> 对第二个矩形进行动画处理，并将 <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> 属性设置为默认值 `false`。  
  
-   使用 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 对第三个矩形进行动画处理，并将 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsCumulative%2A> 属性设置为 `true`。  
  
-   使用 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 对最后一个矩形进行动画处理，并将 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsCumulative%2A> 属性设置为 `false`。  
  
 [!code-xml[timingbehaviors_snip#IsCumulativeWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/IsCumulativeExample.xaml#iscumulativewholepage)]  
  
## 请参阅  
 [向动画起始值添加动画输出值](../../../../docs/framework/wpf/graphics-multimedia/how-to-add-an-animation-output-value-to-an-animation-starting-value.md)   
 [重复动画](../../../../docs/framework/wpf/graphics-multimedia/how-to-repeat-an-animation.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)