---
title: "如何：使 UIElement 呈现为透明或半透明 | Microsoft Docs"
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
  - "不透明度, UIElements 的"
  - "UIElements 的透明度"
  - "UIElements, 不透明度"
  - "UIElements, Transparency — 透明度"
ms.assetid: a49fc8d6-7b32-4f28-9122-39b632a19b4b
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使 UIElement 呈现为透明或半透明
此示例演示如何使 <xref:System.Windows.UIElement> 呈现为透明或半透明。  若要使元素呈现为透明或半透明，请设置它的 <xref:System.Windows.UIElement.Opacity%2A> 属性。  值 `0.0` 会使元素呈现为完全透明，而值 `1.0` 则使元素呈现为完全不透明。  值 `0.5` 使元素呈现为 50% 不透明。其他值可以依次类推。  默认情况下将元素的 <xref:System.Windows.UIElement.Opacity%2A> 设置为 `1.0`。  
  
## 示例  
 下面的示例将按钮的 <xref:System.Windows.UIElement.Opacity%2A> 设置为 `0.25`，从而使该按钮及按钮内容（这里指按钮的文本）呈现为 25% 不透明。  
  
 [!code-xml[brushsamples_snip#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#2)]  
  
 [!code-csharp[brushsamples_procedural_snip#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#2)]  
  
 如果元素内容拥有自己的 <xref:System.Windows.UIElement.Opacity%2A> 设置，则针对包含元素 <xref:System.Windows.UIElement.Opacity%2A> 将这些值相乘。  
  
 下面的示例将按钮的 <xref:System.Windows.UIElement.Opacity%2A> 设置为 `0.25`，并将该按钮中包含的 <xref:System.Windows.Controls.Image> 控件的 <xref:System.Windows.UIElement.Opacity%2A> 设置为 `0.5`。  因此，图像会显示为 12.5% 不透明，即 0.25 \* 0.5 \= 0.125。  
  
 [!code-xml[brushsamples_snip#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#3)]  
  
 [!code-csharp[brushsamples_procedural_snip#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#3)]  
  
 控制元素的不透明度的另一种方法是设置用于绘制该元素的 <xref:System.Windows.Media.Brush> 的不透明度。  使用这种方法，您可以有选择性地改变元素某些部分的不透明度。与使用元素的 <xref:System.Windows.UIElement.Opacity%2A> 属性相比，这更具有性能优势。  下面的示例将用于绘制按钮 <xref:System.Windows.Controls.Control.Background%2A> 的 <xref:System.Windows.Media.SolidColorBrush> 的 <xref:System.Windows.Media.Brush.Opacity%2A> 设置为 `0.25`。  因此，画笔的背景为 25% 不透明，但其内容（按钮的文本）仍保留为 100% 不透明。  
  
 [!code-xml[brushsamples_snip#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#4)]  
  
 [!code-csharp[brushsamples_procedural_snip#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#4)]  
  
 您还可以使用画笔来控制单个颜色的不透明度。  有关颜色和画笔的更多信息，请参见[使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)。  有关演示如何对元素的不透明度进行动画处理的示例，请参见[对元素或画笔的不透明度进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-the-opacity-of-an-element-or-brush.md)。