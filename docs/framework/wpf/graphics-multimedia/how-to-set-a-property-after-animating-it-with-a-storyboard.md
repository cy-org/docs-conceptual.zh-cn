---
title: "如何：在使用演示图板对属性进行动画处理后设置该属性 | Microsoft Docs"
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
  - "动画, 更改属性值"
ms.assetid: 79466556-4dbf-40bd-9c1e-a77613b07077
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：在使用演示图板对属性进行动画处理后设置该属性
在某些情况下，在对属性进行动画处理之后，似乎无法更改该属性的值。  
  
## 示例  
 在下面的示例中，<xref:System.Windows.Media.Animation.Storyboard> 用于对 <xref:System.Windows.Media.SolidColorBrush> 的颜色进行动画处理。  当单击按钮时将触发演示图板。  处理 <xref:System.Windows.Media.Animation.Timeline.Completed> 事件以便在 <xref:System.Windows.Media.Animation.ColorAnimation> 完成时通知程序。  
  
 [!code-xml[timingbehaviors_snip#GraphicsMMButton1Declaration](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton1declaration)]  
  
## 示例  
 在 <xref:System.Windows.Media.Animation.ColorAnimation> 完成之后，程序尝试将画笔的颜色改为蓝色。  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton1Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton1handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton1Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton1handler)]  
  
 上面的代码似乎未起任何作用：画笔仍然保持为黄色，即对画笔进行动画处理的 <xref:System.Windows.Media.Animation.ColorAnimation> 所提供的值。  基础属性值（基值）实际上已改为蓝色。  但是，因为 <xref:System.Windows.Media.Animation.ColorAnimation> 仍然在重写基值，所以有效值（或者说当前值）仍保持为黄色。  如果需要将基值再次变为有效值，则必须禁止动画影响该属性。  使用演示图板动画，可以有三种方法实现此目标：  
  
-   将动画的 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 属性设置为 <xref:System.Windows.Media.Animation.FillBehavior>  
  
-   移除整个演示图板。  
  
-   从单个属性移除动画。  
  
## 将动画的 FillBehavior 属性设置为 Stop  
 通过将 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 设置为 <xref:System.Windows.Media.Animation.FillBehavior>，即通知动画在到达其活动期末尾后停止影响其目标属性。  
  
 [!code-xml[timingbehaviors_snip#GraphicsMMButton2Declaration](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton2declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton2Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton2handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton2Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton2handler)]  
  
## 移除整个演示图板  
 通过使用 <xref:System.Windows.Media.Animation.RemoveStoryboard> 触发器或 <xref:System.Windows.Media.Animation.Storyboard.Remove%2A?displayProperty=fullName> 方法，通知演示图板动画停止影响其目标属性。  此方法与设置 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 属性的不同之处在于：您可以在任何时候移除演示图板，而 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 属性只有在动画到达其活动期末尾时才有效。  
  
 [!code-xml[timingbehaviors_snip#GraphicsMMButton3Declaration](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton3declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton3Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton3handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton3Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton3handler)]  
  
## 从单个属性移除动画  
 禁止动画影响属性的另一种方法是使用正在进行动画处理的对象的 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29> 方法。  将正进行动画处理的属性指定为第一个参数，将 `null` 指定为第二个参数。  
  
 [!code-xml[timingbehaviors_snip#GraphicsMMButton4Declaration](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton4declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton4Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton4handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton4Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton4handler)]  
  
 此方法对于非演示图板动画也有效。  
  
## 请参阅  
 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>   
 <xref:System.Windows.Media.Animation.Storyboard.Remove%2A?displayProperty=fullName>   
 <xref:System.Windows.Media.Animation.RemoveStoryboard>   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)