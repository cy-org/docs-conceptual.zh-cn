---
title: "如何：使用 CompositionTarget 以每帧间隔呈现 | Microsoft Docs"
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
  - "CompositionTarget 对象, 逐个框架呈现"
  - "使用 CompositionTarget 对象逐个框架呈现"
ms.assetid: 701246cd-66b7-4d69-ada9-17b3b433d95d
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用 CompositionTarget 以每帧间隔呈现
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画引擎为创建基于帧的动画提供了许多功能。  但是，在有些应用程序方案中，您需要基于每个帧来以更细的粒度控制呈现。  使用 <xref:System.Windows.Media.CompositionTarget> 对象，可以基于每个帧回调来创建自定义动画。  
  
 <xref:System.Windows.Media.CompositionTarget> 是一个静态类，表示您的应用程序要在其上进行绘制的显示图面。  每次绘制应用程序的场景时，都会引发 <xref:System.Windows.Media.CompositionTarget.Rendering> 事件。  呈现帧速率是指每秒绘制场景的次数。  
  
> [!NOTE]
>  有关使用 <xref:System.Windows.Media.CompositionTarget> 的完整代码示例，请参见 [Using the CompositionTarget Sample](http://go.microsoft.com/fwlink/?LinkID=160045)（使用 CompositionTarget 示例）。  
  
## 示例  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 呈现过程中，会激发 <xref:System.Windows.Media.CompositionTarget.Rendering> 事件。  下面的示例演示如何向 <xref:System.Windows.Media.CompositionTarget> 上的静态 <xref:System.Windows.Media.CompositionTarget.Rendering> 方法中注册 <xref:System.EventHandler> 委托。  
  
 [!code-csharp[CompositionTargetSample#CompositionTarget1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CompositionTargetSample/CSharp/Window1.xaml.cs#compositiontarget1)]
 [!code-vb[CompositionTargetSample#CompositionTarget1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CompositionTargetSample/visualbasic/window1.xaml.vb#compositiontarget1)]  
  
 您可以使用自己的呈现事件处理程序方法创建自定义绘图内容。  每帧调用一次此事件处理程序方法。  每次 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将[可视化树](GTMT)中的持久呈现数据封送到组合场景关系图中时，都会调用您的事件处理程序方法。  另外，如果更改[可视化树](GTMT)将强制更新组合场景关系图，也会调用您的事件处理程序方法。  请注意，计算布局后会调用您的事件处理程序方法。  但是，您可以修改您的事件处理程序方法中的布局，这意味着在呈现之前将再计算一次布局。  
  
 下面的示例演示如何在 <xref:System.Windows.Media.CompositionTarget> 事件处理程序方法中提供自定义绘图。  在本例中，<xref:System.Windows.Controls.Canvas> 的背景色是基于鼠标的坐标位置，用颜色值绘制的。  如果您将鼠标放在 <xref:System.Windows.Controls.Canvas> 内部，则它的背景色将发生变化。  另外，将基于当前的运行时间和所呈现帧的总数来计算平均帧速率。  
  
 [!code-csharp[CompositionTargetSample#CompositionTarget2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CompositionTargetSample/CSharp/Window1.xaml.cs#compositiontarget2)]
 [!code-vb[CompositionTargetSample#CompositionTarget2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CompositionTargetSample/visualbasic/window1.xaml.vb#compositiontarget2)]  
  
 您可能会发现自定义绘图在不同计算机上以不同的速度运行，  这是由于自定义绘图与帧速率有关。  根据所运行的系统以及系统的工作负荷，每秒调用 <xref:System.Windows.Media.CompositionTarget.Rendering> 事件的次数可能会有所不同。  有关为运行 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序的设备确定图形硬件功能和性能的信息，请参见[图形呈现层](../../../../docs/framework/wpf/advanced/graphics-rendering-tiers.md)。  
  
 在激发事件时对呈现 <xref:System.EventHandler> 委托的添加或移除将延迟到事件完成激发之后。  这与基于 <xref:System.MulticastDelegate> 的事件在公共语言运行时 \(CLR\) 中的处理方式一致。  另请注意，无法保证按照任何特定顺序来调用呈现事件。  如果您有多个 <xref:System.EventHandler> 委托依赖特定的顺序，则应当注册一个 <xref:System.Windows.Media.CompositionTarget.Rendering> 事件，并按照正确的顺序自己多路复用这些委托。  
  
## 请参阅  
 <xref:System.Windows.Media.CompositionTarget>   
 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)