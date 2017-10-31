---
title: "缓动函数 | Microsoft Docs"
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
  - "将数学公式应用于动画 [WPF]"
  - "将缓动函数应用于动画 [WPF]"
  - "将应用于动画的数学公式 [WPF]"
  - "真实运动的动画 [WPF]"
  - "缓动函数 [WPF]"
  - "自定义缓动函数 [WPF]"
  - "定义的缓动函数 [WPF]"
  - "自定义缓动函数 [WPF]"
  - "应用动画 [WPF]"
ms.assetid: 075b9c2b-82c4-43fa-b3cd-de0b6236eb38
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 缓动函数
缓动函数允许您将自定义的数学公式应用于动画。 例如，可能想要现实地弹跳或其行为就好像它是在弹簧上的对象。 您可以使用关键帧或甚至 From/To/By 动画来估计这些效果，但它需要占用大量的工作，动画会比使用数学公式不太准确。  
  
 除了通过继承创建您自己的自定义缓动函数外<xref:System.Windows.Media.Animation.EasingFunctionBase>，可以使用运行时提供的若干缓动函数之一来创建常见效果。  
  
-   <xref:System.Windows.Media.Animation.BackEase>︰ 指定的路径中进行动画处理在开始之前将略有收回动画的动作。  
  
-   <xref:System.Windows.Media.Animation.BounceEase>︰ 创建弹跳效果。  
  
-   <xref:System.Windows.Media.Animation.CircleEase>︰ 创建一个动画加速和/或减速使用循环函数。  
  
-   <xref:System.Windows.Media.Animation.CubicEase>︰ 创建一个动画加速和/或减速使用下面的公式*f*( *t*) = *t*<sup>3</sup>。  
  
-   <xref:System.Windows.Media.Animation.ElasticEase>︰ 创建类似于弹簧 rest 直到显示来回振荡的动画。  
  
-   <xref:System.Windows.Media.Animation.ExponentialEase>︰ 创建一个动画加速和/或减速使用指数公式。  
  
-   <xref:System.Windows.Media.Animation.PowerEase>︰ 创建一个动画加速和/或减速使用下面的公式*f*( *t*) = *t*<sup>p</sup> p 是等于<xref:System.Windows.Media.Animation.PowerEase.Power%2A>属性。  
  
-   <xref:System.Windows.Media.Animation.QuadraticEase>︰ 创建一个动画加速和/或减速使用下面的公式*f*( *t*) = *t*<sup>2</sup>。  
  
-   <xref:System.Windows.Media.Animation.QuarticEase>︰ 创建一个动画加速和/或减速使用下面的公式*f*( *t*) = *t*<sup>4</sup>。  
  
-   <xref:System.Windows.Media.Animation.QuinticEase>︰ 创建一个动画加速和/或减速使用下面的公式*f*( *t*) = *t*<sup>5</sup>。  
  
-   <xref:System.Windows.Media.Animation.SineEase>︰ 创建一个动画加速和/或减速使用正弦值的公式。  
  
 您可以浏览下面的示例使用这些缓动函数的行为。  
  
 [运行此示例](http://go.microsoft.com/fwlink/?LinkId=139798&sref=easing_functions_gallery)  
  
 若要将缓动函数应用于动画，使用`EasingFunction`动画的属性指定要应用于该动画的缓动函数。 下面的示例应用<xref:System.Windows.Media.Animation.BounceEase>缓动函数到<xref:System.Windows.Media.Animation.DoubleAnimation>创建弹跳效果。  
  
 [运行此示例](http://go.microsoft.com/fwlink/?LinkId=139798&sref=BounceEase)  
  
 [!code-xml[BounceEase_snippet#BounceEase](../../../../samples/snippets/csharp/VS_Snippets_Wpf/bounceease_snippet/CS/window1.xaml#bounceease)]  
  
 在上一示例中，缓动函数应用于 From/To/By 动画。 您还可以对关键帧动画应用这些缓动函数。 下面的示例演示如何使用关键帧与缓动函数与之关联来创建一个协定呈上升，减速，然后向下展开 （如同下降），然后弹跳至停止的矩形的动画。  
  
 [运行此示例](http://go.microsoft.com/fwlink/?LinkId=139798&sref=EasingFunctionDoubleKeyFrame)  
  
 [!code-xml[EasingFunctionDoubleKeyFrame_snippet#EasingFunctionDoubleKeyFrame](../../../../samples/snippets/csharp/VS_Snippets_Wpf/easingfunctiondoublekeyframe_snippet/CS/window1.xaml#easingfunctiondoublekeyframe)]  
  
 您可以使用<xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A>属性更改的缓动函数的行为方式，即，更改的动画内插方式。 有三个可能的值会使<xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A>:  
  
-   <xref:System.Windows.Media.Animation.EasingMode>︰ 内插遵循与缓动函数相关联的数学公式。  
  
-   <xref:System.Windows.Media.Animation.EasingMode>︰ 内插遵循与缓动函数相关联的公式的 100%减去输出的内插。  
  
-   <xref:System.Windows.Media.Animation.EasingMode>︰ 插值使用<xref:System.Windows.Media.Animation.EasingMode>动画的第一个另一半和<xref:System.Windows.Media.Animation.EasingMode>的第二个另一半。  
  
 下图演示的不同值<xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A>其中*f*( *x*) 表示动画进度和*t*表示时间。  
  
 <xref:System.Windows.Media.Animation.BackEase>  
  
 ![BackEase EasingMode 图。] (../Image/BackEase_Graph.png "BackEase_Graph")  
  
 <xref:System.Windows.Media.Animation.BounceEase>  
  
 ![BounceEase EasingMode 图。] (../Image/BounceEase_Graph.png "BounceEase_Graph")  
  
 <xref:System.Windows.Media.Animation.CircleEase>  
  
 ![CircleEase EasingMode 图。] (../Image/CircleEase_Graph.png "CircleEase_Graph")  
  
 <xref:System.Windows.Media.Animation.CubicEase>  
  
 ![CubicEase EasingMode 图。] (../Image/CubicEase_Graph.png "CubicEase_Graph")  
  
 <xref:System.Windows.Media.Animation.ElasticEase>  
  
 ![不同缓动模式图的 ElasticEase。] (../Image/ElasticEase_Graph.png "ElasticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.ExponentialEase>  
  
 ![不同缓动模式的 ExponentialEase 图。] (../Image/ExponentialEase_Graph.png "ExponentialEase_Graph")  
  
 <xref:System.Windows.Media.Animation.PowerEase>  
  
 ![不同缓动模式图的 QuarticEase。] (../Image/QuarticEase_Graph.png "QuarticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuadraticEase>  
  
 ![不同缓动模式图的 QuadraticEase](../../../../docs/framework/wpf/graphics-multimedia/media/quadraticease-graph.png "QuadraticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuarticEase>  
  
 ![不同缓动模式图的 QuarticEase。] (../Image/QuarticEase_Graph.png "QuarticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuinticEase>  
  
 ![不同缓动模式图的 QuinticEase。] (../Image/QuinticEase_Graph.png "QuinticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.SineEase>  
  
 ![不同 EasingMode 值的 SineEase](../../../../docs/framework/wpf/graphics-multimedia/media/sineease-graph.png "SineEase_Graph")  
  
> [!NOTE]
>  您可以使用<xref:System.Windows.Media.Animation.PowerEase>来创建相同的行为<xref:System.Windows.Media.Animation.CubicEase>， <xref:System.Windows.Media.Animation.QuadraticEase>， <xref:System.Windows.Media.Animation.QuarticEase>，和<xref:System.Windows.Media.Animation.QuinticEase>使用<xref:System.Windows.Media.Animation.PowerEase.Power%2A>属性。 例如，如果你想要使用<xref:System.Windows.Media.Animation.PowerEase>用于替换<xref:System.Windows.Media.Animation.CubicEase>，指定<xref:System.Windows.Media.Animation.PowerEase.Power%2A>值为 3。  
  
 除了使用缓动函数包含在运行时，您可以通过继承创建您自己的自定义缓动函数<xref:System.Windows.Media.Animation.EasingFunctionBase>。 下面的示例演示如何创建简单的自定义缓动函数。 您可以添加您自己的缓动函数通过重写的行为方式的数学逻辑<xref:System.Windows.Media.Animation.EasingFunctionBase.EaseInCore%2A>方法。  
  
 [运行此示例](http://go.microsoft.com/fwlink/?LinkId=139798&sref=CustomEasingFunction)  
  
 [!code-csharp[CustomEasingFunction#CustomEasingFunction](../../../../samples/snippets/csharp/VS_Snippets_Wpf/customeasingfunction/csharp/customlog10easingfunction.cs#customeasingfunction)]
 [!code-vb[CustomEasingFunction#CustomEasingFunction](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/customeasingfunction/visualbasic/customlog10easingfunction.vb#customeasingfunction)]
 [!code-xml[CustomEasingFunction#CustomEasingFunction](../../../../samples/snippets/csharp/VS_Snippets_Wpf/customeasingfunction/csharp/window1.xaml#customeasingfunction)]