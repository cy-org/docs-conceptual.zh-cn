---
title: "Visual Basic 和 WPF 事件处理 | Microsoft Docs"
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
  - "事件处理程序, Visual Basic"
  - "Visual Basic, 事件处理程序"
ms.assetid: ad4eb9aa-3afc-4a71-8cf6-add3fbea54a1
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Visual Basic 和 WPF 事件处理
专门针对 [!INCLUDE[TLA#tla_visualbnet](../../../../includes/tlasharptla-visualbnet-md.md)] 语言，您可以使用语言特定的 `Handles` 关键字将事件处理程序与实例关联，而不是将事件处理程序附加到特性或使用 <xref:System.Windows.UIElement.AddHandler%2A> 方法。  但是，用于将处理程序附加到实例的 `Handles` 方法存在一些限制，因为 `Handles` 语法不支持 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件系统的一些特定[路由事件](GTMT)功能。  
  
## 在 WPF 应用程序中使用“Handles”  
 通过 `Handles` 连接到实例和事件的事件处理程序必须全部在实例的分部类声明中定义，此要求也适用于通过元素上的特性值进行分配的事件处理程序。  只能为具有 <xref:System.Windows.FrameworkContentElement.Name%2A> 属性值（或声明了 [x:Name 指令](../../../../docs/framework/xaml-services/x-name-directive.md)）的页上的元素指定 `Handles`。  这是因为 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的 <xref:System.Windows.FrameworkContentElement.Name%2A> 创建实例引用，该实例引用对于支持 `Handles` 语法所需的*实例.事件* 引用格式是非常必要的。  可用于 `Handles` 且没有 <xref:System.Windows.FrameworkContentElement.Name%2A> 引用的唯一元素是定义分部类的根元素实例。  
  
 您可以通过使用逗号分隔 `Handles` 后面的*实例.事件* 引用，来向多个元素分配相同的处理程序。  
  
 可以使用 `Handles` 将多个处理程序分配给相同的*实例.事件* 引用。  不要对处理程序在 `Handles` 引用中的指定顺序赋予任何重要性；您应假定可以以任何顺序调用处理相同事件的处理程序。  
  
 若要移除声明中使用 `Handles` 添加的处理程序，请调用 <xref:System.Windows.UIElement.RemoveHandler%2A>。  
  
 可以使用 `Handles` 附加[路由事件](GTMT)的处理程序，但前提是将处理程序附加到在其成员表中定义要处理的事件的实例。  对于[路由事件](GTMT)，使用 `Handles` 附加的处理程序遵循的路由规则与附加为 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]特性或使用 <xref:System.Windows.UIElement.AddHandler%2A> 公共签名附加的处理程序遵循的路由规则相同。  这意味着如果事件已标记为已处理（事件数据中的 <xref:System.Windows.RoutedEventArgs.Handled%2A> 属性为 `True`），则在响应该事件实例时不会调用使用 `Handles` 附加的处理程序。  可以通过路由中的另一个元素上的实例处理程序，或者路由中的当前元素或更早元素上的类处理将事件标记为已处理。  对于支持成对隧道\/冒泡事件的输入事件，隧道路由可能已经将事件对标记为已处理。  有关路由事件的更多信息，请参见[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)。  
  
## 用于添加处理程序的“Handles”的限制  
 `Handles` 无法为[附加事件](GTMT)引用处理程序。  您必须对该附加事件使用 `add` 访问器方法，或使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的*类型名称.事件名称* 事件特性。  有关详细信息，请参见[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)。  
  
 对于[路由事件](GTMT)，只能使用 `Handles` 为该事件存在于实例成员表中的实例分配处理程序。  但是，对于一般的路由事件，父元素可以是来自子元素的事件的侦听器，即使该父元素的成员表中没有此事件也是如此。  在特性语法中，这可以通过*类型名称.成员名称* 特性形式来指定，此形式限定哪种类型实际定义要处理的事件。  例如，某个父 `Page`（未定义 `Click` 事件）可以通过分配 `Button.Click` 形式的特性处理程序来侦听按钮单击事件。  但 `Handles` 不支持*类型名称.成员名称* 形式，因为它必须支持与该形式冲突的*实例.事件* 形式。  有关详细信息，请参见[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)。  
  
 `Handles` 无法附加针对标记为已处理的事件而调用的处理程序，  而必须使用代码并调用 <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> 的 `handledEventsToo` 重载。  
  
> [!NOTE]
>  在 XAML 中为相同事件指定事件处理程序时，不要在 [!INCLUDE[vb_current_short](../../../../includes/vb-current-short-md.md)] 代码中使用 `Handles` 语法。  在这种情况下，将调用事件处理程序两次。  
  
## WPF 如何实现“Handles”功能  
 编译[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 页时，中间文件会声明对设置了 <xref:System.Windows.FrameworkContentElement.Name%2A> 属性（或声明了 [x:Name 指令](../../../../docs/framework/xaml-services/x-name-directive.md)）的页中每个元素的 `Friend` `WithEvents` 引用。  每个命名实例都可能是可以通过 `Handles` 分配给处理程序的元素。  
  
> [!NOTE]
>  在 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 中，[!INCLUDE[TLA2#tla_intellisense](../../../../includes/tla2sharptla-intellisense-md.md)] 可以向您显示元素可用于页中的 `Handles` 引用的完成状态。  但是，这可能需要进行一次编译，以便中间文件可以填充所有 `Friends` 引用。  
  
## 请参阅  
 <xref:System.Windows.UIElement.AddHandler%2A>   
 [将路由事件标记为“已处理”和“类处理”](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)