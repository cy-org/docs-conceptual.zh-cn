---
title: "如何：使用演示图板对属性进行动画处理 | Microsoft Docs"
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
  - "动画, 情节提要"
  - "情节提要, 动画"
ms.assetid: f4a314e9-1da2-4367-85fc-1232487efa7a
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用演示图板对属性进行动画处理
此示例演示如何使用 <xref:System.Windows.Media.Animation.Storyboard> 对属性进行动画处理。  若要使用 <xref:System.Windows.Media.Animation.Storyboard> 对属性进行动画处理，请为要进行动画处理的每个属性创建一个动画，另外创建一个 <xref:System.Windows.Media.Animation.Storyboard> 以包含动画。  
  
 属性的类型决定了要使用的动画的类型。  例如，若要对采用 <xref:System.Double> 值的属性进行动画处理，请使用 <xref:System.Windows.Media.Animation.DoubleAnimation>。  <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 和 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A> [附加属性](GTMT)指定要对其应用动画的对象和属性。  
  
 若要启动 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 格式的演示图板，请使用 <xref:System.Windows.Media.Animation.BeginStoryboard> 操作和 <xref:System.Windows.EventTrigger>。  当 <xref:System.Windows.EventTrigger.RoutedEvent%2A> 属性所指定的事件发生时，<xref:System.Windows.EventTrigger> 将开始 <xref:System.Windows.Media.Animation.BeginStoryboard> 操作。  <xref:System.Windows.Media.Animation.BeginStoryboard> 操作将启动 <xref:System.Windows.Media.Animation.Storyboard>。  
  
 下面的示例使用 <xref:System.Windows.Media.Animation.Storyboard> 对象对两个 <xref:System.Windows.Controls.Button> 控件进行动画处理。  为了使第一个按钮的大小发生变化，将对其 <xref:System.Windows.FrameworkElement.Width%2A> 进行动画处理。  为了使第二个按钮的颜色发生变化，将使用 <xref:System.Windows.Media.SolidColorBrush> 的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 属性来设置动画处理的按钮的 <xref:System.Windows.Controls.Control.Background%2A>。  
  
## 示例  
 [!code-xml[AnimatePropertyStoryboards#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/AnimatePropertyStoryboards/XAML/StoryboardExample.xaml#1)]  
  
> [!NOTE]
>  虽然动画能够将 <xref:System.Windows.FrameworkElement> 对象（如 <xref:System.Windows.Controls.Control> 或 <xref:System.Windows.Controls.Panel>）和 <xref:System.Windows.Freezable> 对象（如 <xref:System.Windows.Media.Brush> 或 <xref:System.Windows.Media.Transform>）作为处理目标，但只有框架元素才具有 <xref:System.Windows.FrameworkElement.Name%2A> 属性。  如上面的示例所示，若要为可冻结的对象指定一个名称以便动画能够将此对象作为处理目标，请使用 [x:Name 指令](../../../../docs/framework/xaml-services/x-name-directive.md)。  
  
 如果使用代码，则必须为 <xref:System.Windows.FrameworkElement> 创建 <xref:System.Windows.NameScope>，并向该 <xref:System.Windows.FrameworkElement> 注册要进行动画处理的对象的名称。  若要在代码中启动动画，请将 <xref:System.Windows.Media.Animation.BeginStoryboard> 操作和 <xref:System.Windows.EventTrigger> 一起使用。  （可选）您可以使用事件处理程序和 <xref:System.Windows.Media.Animation.Storyboard> 的 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法。  下面的示例演示如何使用 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法。  
  
 [!code-csharp[AnimatePropertyStoryboards#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimatePropertyStoryboards/CSharp/StoryboardExample.cs#11)]
 [!code-vb[AnimatePropertyStoryboards#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AnimatePropertyStoryboards/VisualBasic/StoryboardExample.vb#11)]  
  
 有关动画和演示图板的更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
 如果使用代码，则并非只能使用 <xref:System.Windows.Media.Animation.Storyboard> 对象对属性进行动画处理。  有关更多信息和示例，请参见 [在不使用演示图板的情况下对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md) 和 [使用 AnimationClock 对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-an-animationclock.md)。