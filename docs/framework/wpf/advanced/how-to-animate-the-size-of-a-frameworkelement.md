---
title: "如何：对 FrameworkElement 的大小进行动画处理 | Microsoft Docs"
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
  - "动画, FrameworkElement 大小"
  - "FrameworkElement, 对大小进行动画处理"
ms.assetid: d4cd5a13-c20d-4a6f-a2ba-14f2c9ce4cef
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：对 FrameworkElement 的大小进行动画处理
若要对 <xref:System.Windows.FrameworkElement> 的大小进行动画处理，可以对它的 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性进行动画处理，或者使用经过动画处理的 <xref:System.Windows.Media.ScaleTransform>。  
  
 下面的示例使用这两种方法对两个按钮的大小进行动画处理。  对于第一个按钮，通过对它的 <xref:System.Windows.FrameworkElement.Width%2A> 属性进行动画处理来调整其大小；对于第二个按钮，通过对应用于它的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性的 <xref:System.Windows.Media.ScaleTransform> 进行动画处理来调整大小。  每个按钮都包含一段文本。  最初，这些文本在两个按钮中以相同的方式显示，但是在按钮的大小经过调整后，第二个按钮中的文本将发生扭曲。  
  
## 示例  
 [!code-xml[transformanimations_snip#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/transformanimations_snip/XAML/AnimatingSizeExample.xaml#1)]  
  
 对元素进行转换时，整个元素及其内容也将进行转换。  当您直接改变元素的大小时（就像对第一个按钮所执行的操作），除非元素的大小和位置取决于其父元素的大小，否则元素内容的大小不会进行调整。  
  
 在对元素的大小进行动画处理时，与直接对元素的 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 进行动画处理相比，向元素的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性应用经过动画处理的转换具有更好的性能，因为 <xref:System.Windows.UIElement.RenderTransform%2A> 属性不会触发布局处理过程。  
  
 有关对属性进行动画处理的更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  有关转换的更多信息，请参见[变换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)。