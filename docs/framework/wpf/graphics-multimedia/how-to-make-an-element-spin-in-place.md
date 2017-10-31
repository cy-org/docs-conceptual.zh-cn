---
title: "如何：使元素就地旋转 | Microsoft Docs"
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
  - "类, DoubleAnimation"
  - "类, RotateTransform"
  - "DoubleAnimation 类"
  - "图形, 旋转元素"
  - "RotateTransform 类"
  - "旋转元素"
ms.assetid: 1f011976-8b07-4c31-9faf-019e0ddaa24c
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使元素就地旋转
此示例演示如何使用 <xref:System.Windows.Media.RotateTransform> 和 <xref:System.Windows.Media.Animation.DoubleAnimation> 来使某个元素旋转。  
  
 下面的示例将 <xref:System.Windows.Media.RotateTransform> 应用于该元素的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性。  该示例使用 <xref:System.Windows.Media.Animation.DoubleAnimation> 来对 <xref:System.Windows.Media.RotateTransform> 的 <xref:System.Windows.Media.RotateTransform.Angle%2A> 进行动画处理。  为了使该元素就地旋转，此示例将该元素的 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 属性设置为点 \(0.5, 0.5\)。  
  
## 示例  
 [!code-xml[transformanimations_snip#11](../../../../samples/snippets/xaml/VS_Snippets_Wpf/transformanimations_snip/XAML/RotateAboutCenterExample.xaml#11)]  
  
 有关包括更多转换示例的完整示例，请参见 [2\-D Transforms Sample](http://go.microsoft.com/fwlink/?LinkID=158252)（二维转换示例）。  
  
## 请参阅  
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)