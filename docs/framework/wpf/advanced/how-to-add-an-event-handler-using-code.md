---
title: "如何：使用代码添加事件处理程序 | Microsoft Docs"
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
  - "事件处理程序, 添加"
  - "XAML, 添加事件处理程序"
ms.assetid: 269c61e0-6bd9-4291-9bed-1c5ee66da486
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：使用代码添加事件处理程序
此示例演示如何使用代码为元素添加事件处理程序。  
  
 如果您希望为某个 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 元素添加事件处理程序，而包含该元素的标记页面已经加载，则必须使用代码添加该处理程序。  或者，如果您正在完全使用代码为应用程序生成元素树，而没有使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 声明任何元素，则可以调用特定的方法将事件处理程序添加到构造的元素树中。  
  
## 示例  
 下面的示例向最初使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 定义的现有页面上添加一个新的 <xref:System.Windows.Controls.Button>。  代码隐藏文件实现一个事件处理程序方法，然后添加该方法添加为 <xref:System.Windows.Controls.Button> 的一个新的事件处理程序。  
  
 [!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)] 示例使用 `+=` 运算符为事件指定处理程序。  这与 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 事件处理模型中用来指定处理程序的运算符相同。  [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)] 不支持使用此运算符添加事件处理程序。  相反，它要求使用下列两种方法之一：  
  
-   将 <xref:System.Windows.UIElement.AddHandler%2A> 方法和 `AddressOf` 运算符结合使用，以引用事件处理程序实现。  
  
-   使用 `Handles` 关键字作为事件处理程序定义的一部分。  此处未演示此方法；请参见 [Visual Basic 和 WPF 事件处理](../../../../docs/framework/wpf/advanced/visual-basic-and-wpf-event-handling.md)。  
  
 [!code-xml[RoutedEventAddRemoveHandler#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[RoutedEventAddRemoveHandler#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventAddRemoveHandler#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/VisualBasic/default.xaml.vb#handler)]  
  
> [!NOTE]
>  在最初分析的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页面上添加一个事件处理程序要简单得多。  在要添加事件处理程序的对象元素中，添加一个与您要处理的事件的名称匹配的特性。  然后将该特性的值指定为您在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页面的代码隐藏文件中定义的事件处理程序方法的名称。  有关更多信息，请参见 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)或[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)。  
  
## 请参阅  
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/events-how-to-topics.md)