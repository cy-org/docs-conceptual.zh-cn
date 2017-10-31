---
title: "如何：使用关键帧对 Matrix 进行动画处理 | Microsoft Docs"
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
  - "动画, 使用关键帧对 Matrix 属性进行动画处理"
  - "关键帧, 对 Matrix 属性进行动画处理"
  - "Matrix 属性, 使用关键帧进行动画处理"
ms.assetid: b851a4c7-ecb1-420e-9203-83e7afd037fd
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用关键帧对 Matrix 进行动画处理
此示例演示如何使用关键帧对 <xref:System.Windows.Media.MatrixTransform> 的 <xref:System.Windows.Media.MatrixTransform.Matrix%2A> 属性进行动画处理。  
  
## 示例  
 下面的示例使用 <xref:System.Windows.Media.Animation.MatrixAnimationUsingKeyFrames> 类对 <xref:System.Windows.Media.MatrixTransform> 的 <xref:System.Windows.Media.MatrixTransform.Matrix%2A> 属性进行动画处理。  该示例使用 <xref:System.Windows.Media.MatrixTransform> 对象来转换 <xref:System.Windows.Controls.Button> 的外观和位置。  
  
 此动画使用 <xref:System.Windows.Media.Animation.DiscreteMatrixKeyFrame> 类来创建两个关键帧并对它们执行以下操作：  
  
1.  在头 0.2 秒内对第一个 <xref:System.Windows.Media.Matrix> 进行动画处理。  此示例更改 <xref:System.Windows.Media.Matrix> 的 <xref:System.Windows.Media.Matrix.M11%2A> 和 <xref:System.Windows.Media.Matrix.M12%2A> 属性。  此更改导致按钮拉伸并扭曲。  此示例还更改 <xref:System.Windows.Media.Matrix.OffsetX%2A> 和 <xref:System.Windows.Media.Matrix.OffsetY%2A> 属性，使按钮改变位置。  
  
2.  在 1.0 秒处对第二个 <xref:System.Windows.Media.Matrix> 进行动画处理。  此按钮移到其他位置，同时此按钮不再是扭曲或拉伸的。  
  
3.  无限地重复此动画。  
  
> [!NOTE]
>  从 <xref:System.Windows.Media.Animation.DiscreteMatrixKeyFrame> 对象派生的关键帧创建值之间的突然跳变，也就是说，动画的运动是不平稳的。  
  
 [!code-xml[keyframes_snip#MatrixAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/MatrixAnimationUsingKeyFramesExample.xaml#matrixanimationusingkeyframeswholepage)]  
  
 有关完整示例，请参见 [KeyFrame Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160012)（KeyFrame 动画示例）。  
  
## 请参阅  
 <xref:System.Windows.Media.MatrixTransform.Matrix%2A>   
 <xref:System.Windows.Media.MatrixTransform>   
 [关键帧动画概述](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [关键帧动画帮助主题](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)