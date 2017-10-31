---
title: "如何：在样式中进行动画处理 | Microsoft Docs"
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
  - "动画, 属性, 在样式中"
  - "样式, 对属性进行动画处理"
ms.assetid: 6a791f3d-6b1f-4972-a2f9-35880bcfd954
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在样式中进行动画处理
本主题中的示例演示如何对样式中的属性进行动画处理。  在样式中进行动画处理时，只能直接以定义了样式的框架元素作为目标。  若要以可冻结的对象为目标，必须从带样式元素的属性“暂且记下”。  
  
 在下面的示例中，在样式中定义了几个动画，并将这些动画应用于 <xref:System.Windows.Controls.Button>。  当用户将鼠标移到按钮上时，它会反复从不透明淡化为半透明并从半透明淡化为不透明。  当用户将鼠标移出按钮时，按钮会变得完全不透明。  当按钮被单击时，它的背景色会再次从橙色改为黑白色。  由于不能直接以用来绘制按钮的 <xref:System.Windows.Media.SolidColorBrush> 作为目标，因此该 SolidColorBrush 只能通过从按钮的 <xref:System.Windows.Controls.Control.Background%2A> 属性“草草记下”来访问。  
  
## 示例  
 [!code-xml[timingbehaviors_snip#21](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StyleStoryboardsExample.xaml#21)]  
  
 请注意，在样式中进行动画处理时，可以将不存在的对象作为目标。  例如，假设您的样式使用 <xref:System.Windows.Media.SolidColorBrush> 来设置 Button 的背景属性，但是在某个点，该样式被重写，用 <xref:System.Windows.Media.LinearGradientBrush> 设置了该按钮的背景。  尝试对 <xref:System.Windows.Media.SolidColorBrush> 进行动画处理将不会引发异常；动画将只是自行失败。  
  
 有关演示图板目标设定语法的更多信息，请参见[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。  有关动画的更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  有关样式的更多信息，请参见[样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。