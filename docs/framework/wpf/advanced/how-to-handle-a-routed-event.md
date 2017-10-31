---
title: "如何：处理路由事件 | Microsoft Docs"
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
  - "冒泡事件"
  - "路由事件, 处理"
ms.assetid: 157787b4-f469-4047-8777-5b034145f32e
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# 如何：处理路由事件
本示例演示[冒泡](GTMT)事件的工作方式，以及如何编写可处理[路由事件](GTMT)数据的处理程序。  
  
## 示例  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的元素以[元素树](GTMT)结构形式排列。  父元素可以参与处理最初由元素树中的子元素引发的事件，  这是由于存在[事件路由](GTMT)。  
  
 路由事件通常遵循以下两个路由策略之一：[冒泡](GTMT)和[隧道](GTMT)。  下面的示例将重点放在[冒泡](GTMT)事件上，并且使用 <xref:System.Windows.Controls.Primitives.ButtonBase.Click?displayProperty=fullName> 事件来演示路由的工作方式。  
  
 下面的示例创建两个 <xref:System.Windows.Controls.Button> 控件并使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 特性语法向公用的父元素（在本示例中为 <xref:System.Windows.Controls.StackPanel>）附加事件处理程序。  本示例使用特性语法向 <xref:System.Windows.Controls.StackPanel> 父元素附加事件处理程序，而不是为每个 <xref:System.Windows.Controls.Button> 子元素都附加一个事件处理程序。  这个事件处理模式演示了如何使用事件路由技术来减少需要附加处理程序的元素数量。  每个 <xref:System.Windows.Controls.Button> 的所有[冒泡](GTMT)事件都通过父元素进行路由。  
  
 请注意，在父 <xref:System.Windows.Controls.StackPanel> 元素上，指定为特性的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件名称可通过命名 <xref:System.Windows.Controls.Button> 类来进行部分限定。  <xref:System.Windows.Controls.Button> 类是一个 <xref:System.Windows.Controls.Primitives.ButtonBase> 派生类，它在其成员列表中有一个 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件。  如果要处理的事件不在附加有路由事件处理程序的元素的成员列表中，则有必要使用这种部分限定技术来附加事件处理程序。  
  
 [!code-xml[RoutedEventHandle#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventHandle/CSharp/default.xaml#xaml)]  
  
 下面的示例处理 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件。  该示例报告哪个元素处理该事件以及哪个元素引发该事件。  当用户单击任一按钮时，会执行事件处理程序。  
  
 [!code-csharp[RoutedEventHandle#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventHandle/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventHandle#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventHandle/VisualBasic/MainWindow.xaml.vb#handler)]  
  
## 请参阅  
 <xref:System.Windows.RoutedEvent>   
 [输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/events-how-to-topics.md)   
 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)