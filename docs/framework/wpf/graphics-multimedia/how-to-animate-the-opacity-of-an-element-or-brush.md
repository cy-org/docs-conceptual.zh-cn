---
title: "如何：对元素或画笔的不透明度进行动画处理 | Microsoft Docs"
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
  - "动画, Opacity 属性"
  - "不透明度, 动画处理"
ms.assetid: 572af23b-39dd-48d1-9db5-4bca56a4b3d3
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：对元素或画笔的不透明度进行动画处理
若要使框架元素淡入和淡出视野，可以对其 <xref:System.Windows.UIElement.Opacity%2A> 属性进行动画处理，或者对用于绘制该框架元素的 <xref:System.Windows.Media.Brush>（画笔）的 <xref:System.Windows.Media.Brush.Opacity%2A> 属性进行动画处理。  对元素的不透明度进行动画处理，可以令该元素及其子元素淡入和淡出视野，不过，如果对用于绘制元素的画笔进行动画处理，则您可以选择使元素的哪部分淡入淡出。  例如，您可以对用于绘制按钮背景的画笔的不透明度进行动画处理。  这会导致按钮的背景淡入和淡出视野，同时使其文本完全不透明。  
  
> [!NOTE]
>  对 <xref:System.Windows.Media.Brush> 的 <xref:System.Windows.Media.Brush.Opacity%2A> 进行动画处理在性能上要优于对元素的 <xref:System.Windows.UIElement.Opacity%2A> 属性进行动画处理。  
  
 在下面的示例中，将对两个按钮进行动画处理，使其淡入和淡出视野。  第一个 <xref:System.Windows.Controls.Button> 的 Opacity 在 5 秒的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 内以动画形式从 `1.0` 过渡到 `0.0`。  第二个按钮也进行了动画处理，不过是对用于绘制其 <xref:System.Windows.Controls.Control.Background%2A> 的 SolidColorBrush 的 Opacity 进行动画处理，而不是对整个按钮的 Opacity 进行动画处理。  当此示例运行时，第一个按钮会整个地淡入和淡出视野，而第二个按钮只有背景部分淡入和淡出视野。  其文本和边框则保持完全不透明状态。  
  
## 示例  
 [!code-xml[timingbehaviors_snip#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/OpacityAnimationExample.xaml#10)]  
  
 此示例省略了代码。  完整的示例还演示如何对 <xref:System.Windows.Media.LinearGradientBrush> 内的 <xref:System.Windows.Media.Color> 的不透明度进行动画处理。  有关完整示例，请参见 [Animating the Opacity of an Element Sample](http://go.microsoft.com/fwlink/?LinkID=159968)（对元素的不透明度进行动画处理示例）。