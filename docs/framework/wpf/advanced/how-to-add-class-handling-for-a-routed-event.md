---
title: "如何：为路由事件添加类处理 | Microsoft Docs"
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
  - "类处理程序, 路由事件"
  - "路由事件, 类处理程序"
  - "task_core_add_class_handling_routed_event"
ms.assetid: 15b7b06c-9112-4ee5-b30a-65d10c5c5df6
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：为路由事件添加类处理
在路由中的任何给定节点上，路由事件可以由类处理程序或实例处理程序来处理。  首先调用类处理程序，类实现功能可以使用它们来禁止事件进行实例处理，或者在基类所拥有的事件上引入其他特定于事件的行为。  本示例阐释了两个紧密相关的、用来实现类处理程序的技术。  
  
## 示例  
 本示例使用一个基于 <xref:System.Windows.Controls.Canvas> 面板的自定义类。  应用程序的基本前提就是，在调用子元素类或其上的任何实例处理程序之前，自定义类在其子元素上引入行为（包括解释任何鼠标左键单击并将它们标记为“已处理”）。  
  
 <xref:System.Windows.UIElement> 类公开了一个虚方法，使用该虚方法，只需通过重写 <xref:System.Windows.UIElement.PreviewMouseLeftButtonDown> 事件即可对该事件进行类处理。  当这样的虚方法可以在类层次结构的某处使用时，这是实现类处理的最简单方法。  下面的代码演示如何在从 <xref:System.Windows.Controls.Canvas> 派生的“MyEditContainer”中实现 <xref:System.Windows.UIElement.OnPreviewMouseLeftButtonDown%2A>。  该实现在参数中将事件标记为“已处理”，然后添加一些代码，以便为源元素提供一个基本的可见变化。  
  
 [!code-csharp[ClassHandling#OnStarClassHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ClassHandling/CSharp/SDKSampleLibrary/class1.cs#onstarclasshandler)]
 [!code-vb[ClassHandling#OnStarClassHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ClassHandling/visualbasic/sdksamplelibrary/class1.vb#onstarclasshandler)]  
  
 如果基类或者这个特定方法没有虚方法，则可以使用 <xref:System.Windows.EventManager> 类 <xref:System.Windows.EventManager.RegisterClassHandler%2A> 的实用工具方法直接添加类处理。  此方法只应当从正在添加类处理的类的静态初始化内部调用。  下面的示例为 <xref:System.Windows.UIElement.PreviewMouseLeftButtonDown> 添加另一个处理程序，在这种情况下，注册类就是自定义类。  反过来，在使用虚方法时，注册类实际上是 <xref:System.Windows.UIElement> 基类。  如果基类和子类均注册了类处理功能，则将首先调用子类的处理程序。  应用程序中的行为将是该处理程序首先显示其消息框，随后将显示虚方法处理程序中的可视变化。  
  
 [!code-csharp[ClassHandling#StaticAndRegisterClassHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ClassHandling/CSharp/SDKSampleLibrary/class1.cs#staticandregisterclasshandler)]
 [!code-vb[ClassHandling#StaticAndRegisterClassHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ClassHandling/visualbasic/sdksamplelibrary/class1.vb#staticandregisterclasshandler)]  
  
## 请参阅  
 <xref:System.Windows.EventManager>   
 [将路由事件标记为“已处理”和“类处理”](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)   
 [处理路由事件](../../../../docs/framework/wpf/advanced/how-to-handle-a-routed-event.md)   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)