---
title: "如何：向文本应用动画 | Microsoft Docs"
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
  - "动画, 文本"
  - "版式, 动画"
ms.assetid: eec3d26c-0a21-420f-8012-671621c47089
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：向文本应用动画
动画可以更改应用程序中文本的显示和外观。  下面的示例使用不同类型的动画来影响 <xref:System.Windows.Controls.TextBlock> 控件中文本的显示。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.Animation.DoubleAnimation> 对文本块的宽度进行动画处理。  宽度值从文本块的宽度更改为 0，持续时间为 10 秒，然后再改回其宽度值并继续。  这种动画会创建一个擦除效果。  
  
 [!code-xml[TextAnimationSample#TextAnimationSample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextAnimationSample/CS/Window1.xaml#textanimationsample1)]  
  
 下面的示例使用 <xref:System.Windows.Media.Animation.DoubleAnimation> 对文本块的不透明度进行动画处理。  不透明度值从 1.0 更改为 0，持续时间为 5 秒，然后再改回其不透明度值并继续。  
  
 [!code-xml[TextAnimationSample#TextAnimationSample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextAnimationSample/CS/Window1.xaml#textanimationsample2)]  
  
 下图演示了 <xref:System.Windows.Controls.TextBlock> 控件更改其透明度的效果，其中不透明度的值从 `1.00` 更改为 `0.00`，时间间隔为 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 所定义的 5 秒。  
  
 ![文本不透明度从 1.00 改为 0.00](../../../../docs/framework/wpf/advanced/media/fadedtext01.png "FadedText01")  
从 1.00 更改为 0.00 的文本不透明度  
  
 下面的示例使用 <xref:System.Windows.Media.Animation.ColorAnimation> 对文本块的前景色进行动画处理。  前景颜色值从一种颜色更改为另一种颜色，持续时间为 5 秒，然后返回到原来的颜色值并继续。  
  
 [!code-xml[TextAnimationSample#TextAnimationSample3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextAnimationSample/CS/Window1.xaml#textanimationsample3)]  
  
 下面的代码示例使用 <xref:System.Windows.Media.Animation.DoubleAnimation> 来旋转文本块。  文本块执行完全旋转，持续时间为 20 秒，然后继续重复该旋转。  
  
 [!code-xml[TextAnimationSample#TextAnimationSample4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextAnimationSample/CS/Window1.xaml#textanimationsample4)]  
  
## 请参阅  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)