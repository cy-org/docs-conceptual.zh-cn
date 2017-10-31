---
title: "如何：创建自定义路由事件 | Microsoft Docs"
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
  - "创建, 路由事件"
  - "事件, 路由"
  - "路由事件, 创建"
ms.assetid: b79f459a-1c3f-4045-b2d4-1659cc8eaa3c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：创建自定义路由事件
若要使您的自定义事件支持[事件路由](GTMT)，需要使用 <xref:System.Windows.EventManager.RegisterRoutedEvent%2A> 方法注册 <xref:System.Windows.RoutedEvent>。  本示例演示创建自定义路由事件的基本原理。  
  
## 示例  
 如下面的示例所示，首先使用 <xref:System.Windows.EventManager.RegisterRoutedEvent%2A> 方法注册一个 <xref:System.Windows.RoutedEvent>。  按照约定，<xref:System.Windows.RoutedEvent> 静态字段名称应当以后缀 ***Event*** 结束。  在本示例中，事件的名称是 `Tap`，事件的路由策略是 <xref:System.Windows.RoutingStrategy>。  在注册调用之后，可以为该事件提供添加和移除[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 事件访问器。  
  
 请注意，尽管该事件在本特定示例中是通过 `OnTap` 虚方法引发的，但您引发事件的方式或者事件响应更改的方式取决于您的需要。  
  
 还要注意，本示例主要实现 <xref:System.Windows.Controls.Button> 的一整个子类；该子类是作为单独的程序集构建的，之后将在单独的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 页上实例化为一个自定义类。  这是为了说明这样一个概念：创建子类的控件可以插入到由其他控件组成的树中，在这种情况下，这些控件上的自定义事件具有与任何固有的 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 元素完全相同的事件路由功能。  
  
 [!code-csharp[RoutedEventCustom#CustomClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventCustom/CSharp/SDKSampleLibrary/class1.cs#customclass)]
 [!code-vb[RoutedEventCustom#CustomClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventCustom/VB/SDKSampleLibrary/Class1.vb#customclass)]  
  
 [!code-xml[RoutedEventCustom#Page](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventCustom/CSharp/RoutedEventCustomApp/default.xaml#page)]  
  
 隧道事件是以这种方式创建的，但在注册调用中，<xref:System.Windows.RoutedEvent.RoutingStrategy%2A> 设置为 <xref:System.Windows.RoutingStrategy>。  按照约定，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的隧道事件以单词“Preview”开头。  
  
 若要查看说明冒泡事件的工作原理的示例，请参见[处理路由事件](../../../../docs/framework/wpf/advanced/how-to-handle-a-routed-event.md)。  
  
## 请参阅  
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)