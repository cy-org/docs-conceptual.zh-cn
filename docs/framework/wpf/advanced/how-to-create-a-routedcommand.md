---
title: "如何：创建 RoutedCommand | Microsoft Docs"
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
  - "类, RoutedCommand, 创建"
  - "创建, RoutedCommand 类"
  - "RoutedCommand 类, 创建"
ms.assetid: aaf6979f-69ab-406f-979f-5766daa85fa0
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：创建 RoutedCommand
此示例通过创建一个 <xref:System.Windows.Input.ExecutedRoutedEventHandler> 和一个 <xref:System.Windows.Input.CanExecuteRoutedEventHandler> 并将它们附加到 <xref:System.Windows.Input.CommandBinding>，演示如何创建自定义 <xref:System.Windows.Input.RoutedCommand> 以及如何实现该自定义命令。  有关设置命令的更多信息，请参见[命令概述](../../../../docs/framework/wpf/advanced/commanding-overview.md)。  
  
## 示例  
 创建 <xref:System.Windows.Input.RoutedCommand> 的第一步是定义并实例化该命令。  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCommandDefinition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcommanddefinition)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCommandDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcommanddefinition)]  
  
 为了在应用程序中使用该命令，必须创建定义该命令的行为的事件处理程序  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewExecuted](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewexecuted)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewExecuted](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewexecuted)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCanExecute](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcanexecute)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCanExecute](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcanexecute)]  
  
 接下来，创建一个 <xref:System.Windows.Input.CommandBinding>，它将该命令与事件处理程序关联。  在指定的对象上创建 <xref:System.Windows.Input.CommandBinding>。  此对象定义元素树中 <xref:System.Windows.Input.CommandBinding> 的范围  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewWindowCommandBindingXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewwindowcommandbindingxaml)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCustomCommandBindingCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcustomcommandbindingcodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCustomCommandBindingCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcustomcommandbindingcodebehind)]  
  
 最后一步是调用该命令。  调用命令的一种方式是将该命令与某个 <xref:System.Windows.Input.ICommandSource>（例如 <xref:System.Windows.Controls.Button>）关联。  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewcustomcommandsourcexaml)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcustomcommandsourcecodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcustomcommandsourcecodebehind)]  
  
 单击该 Button 时，将调用自定义 <xref:System.Windows.Input.RoutedCommand> 上的 <xref:System.Windows.Input.RoutedCommand.Execute%2A> 方法。  <xref:System.Windows.Input.RoutedCommand> 将引发 <xref:System.Windows.Input.CommandManager.PreviewExecuted> 和 <xref:System.Windows.Input.CommandManager.Executed> 路由事件。  这些事件会遍历元素树，以查找该特定命令的 <xref:System.Windows.Input.CommandBinding>。  如果找到 <xref:System.Windows.Input.CommandBinding>，则调用与 <xref:System.Windows.Input.CommandBinding> 关联的 <xref:System.Windows.Input.ExecutedRoutedEventHandler>。  
  
## 请参阅  
 <xref:System.Windows.Input.RoutedCommand>   
 [命令概述](../../../../docs/framework/wpf/advanced/commanding-overview.md)