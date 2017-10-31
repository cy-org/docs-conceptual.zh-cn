---
title: "如何：启用命令 | Microsoft Docs"
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
  - "CommandBindings"
  - "命令"
ms.assetid: d8016266-58d9-48f7-8298-a86b7ed49fbd
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：启用命令
下面的示例演示如何在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中使用命令设置功能。  该示例演示如何将 <xref:System.Windows.Input.RoutedCommand> 与 <xref:System.Windows.Controls.Button> 关联，如何创建 <xref:System.Windows.Input.CommandBinding>，以及如何创建实现 <xref:System.Windows.Input.RoutedCommand> 的事件处理程序。  有关设置命令的更多信息，请参见[命令概述](../../../../docs/framework/wpf/advanced/commanding-overview.md)。  
  
## 示例  
 代码的第一部分创建由 <xref:System.Windows.Controls.Button> 和 <xref:System.Windows.Controls.StackPanel> 组成的[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]，并创建一个将命令处理程序与 <xref:System.Windows.Input.RoutedCommand> 关联的 <xref:System.Windows.Input.CommandBinding>。  
  
 <xref:System.Windows.Controls.Button> 的 <xref:System.Windows.Input.ICommandSource.Command%2A> 属性与 <xref:System.Windows.Input.ApplicationCommands.Close%2A> 命令关联。  
  
 <xref:System.Windows.Input.CommandBinding> 添加到根 <xref:System.Windows.Window> 的 <xref:System.Windows.Input.CommandBindingCollection> 中。  <xref:System.Windows.Input.CommandBinding.Executed> 和 <xref:System.Windows.Input.CommandBinding.CanExecute> 事件处理程序附加到此绑定并与 <xref:System.Windows.Input.ApplicationCommands.Close%2A> 命令关联。  
  
 没有 <xref:System.Windows.Input.CommandBinding> 就没有命令逻辑，而只是存在调用命令的机制。  在单击 <xref:System.Windows.Controls.Button> 时，会针对命令目标引发 <xref:System.Windows.Input.CommandManager.PreviewExecuted> <xref:System.Windows.RoutedEvent>，之后将引发 <xref:System.Windows.Input.CommandManager.Executed> <xref:System.Windows.RoutedEvent>。  这些事件会遍历元素树，以查找该特定命令的 <xref:System.Windows.Input.CommandBinding>。  值得注意的是，由于 <xref:System.Windows.RoutedEvent> 会在元素树中执行隧道和冒泡操作，因此一定要注意 <xref:System.Windows.Input.CommandBinding> 的放置位置。  如果 <xref:System.Windows.Input.CommandBinding> 位于命令目标的同级，或者它所在的节点不在 <xref:System.Windows.RoutedEvent> 的路由上，将不会访问 <xref:System.Windows.Input.CommandBinding>。  
  
 [!code-xml[EnableCloseCommand#CloseCommandBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml#closecommandbinding)]  
  
 [!code-csharp[EnableCloseCommand#CloseCommandBindingCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml.cs#closecommandbindingcodebehind)]
 [!code-vb[EnableCloseCommand#CloseCommandBindingCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/EnableCloseCommand/VisualBasic/Window1.xaml.vb#closecommandbindingcodebehind)]  
  
 代码的第二部分实现 <xref:System.Windows.Input.CommandManager.Executed> 和 <xref:System.Windows.Input.CommandBinding.CanExecute> 事件处理程序。  
  
 <xref:System.Windows.Input.CommandManager.Executed> 处理程序调用一个方法来关闭已打开的文件。  <xref:System.Windows.Input.CommandBinding.CanExecute> 处理程序调用一个方法来确定文件是否处于打开状态。  如果文件处于打开状态，<xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A> 将设置为 `true`；否则将设置为 `false`。  
  
 [!code-csharp[EnableCloseCommand#CloseCommandHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml.cs#closecommandhandler)]
 [!code-vb[EnableCloseCommand#CloseCommandHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/EnableCloseCommand/VisualBasic/Window1.xaml.vb#closecommandhandler)]  
  
## 请参阅  
 [命令概述](../../../../docs/framework/wpf/advanced/commanding-overview.md)