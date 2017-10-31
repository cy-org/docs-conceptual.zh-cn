---
title: "如何：将命令挂钩到不支持命令的控件 | Microsoft Docs"
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
  - "类, 控件, 附加 RoutedCommand"
  - "类, RoutedCommand, 附加到 Control"
  - "Control 类, 附加 RoutedCommand"
  - "RoutedCommand 类, 附加到 Control"
ms.assetid: dad08f64-700b-46fb-ad3f-fbfee95f0dfe
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：将命令挂钩到不支持命令的控件
下面的示例演示如何将 <xref:System.Windows.Input.RoutedCommand> 挂钩到没有为该命令提供内置支持的 <xref:System.Windows.Controls.Control>。  有关将多个命令挂钩到多个源的完整示例，请参见 [Create a Custom RoutedCommand Sample](http://go.microsoft.com/fwlink/?LinkID=159980)（创建自定义 RoutedCommand 示例）示例。  
  
## 示例  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供了应用程序程序员经常遇到的常见命令库。  构成此命令库的类有：<xref:System.Windows.Input.ApplicationCommands>、<xref:System.Windows.Input.ComponentCommands>、<xref:System.Windows.Input.NavigationCommands>、<xref:System.Windows.Input.MediaCommands> 和 <xref:System.Windows.Documents.EditingCommands>。  
  
 组成这些类的静态 <xref:System.Windows.Input.RoutedCommand> 对象不提供命令逻辑。  命令的逻辑通过 <xref:System.Windows.Input.CommandBinding> 与命令关联。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的许多控件为命令库中的某些命令提供内置支持。  例如，<xref:System.Windows.Controls.TextBox> 支持许多应用程序编辑命令，如 <xref:System.Windows.Input.ApplicationCommands.Paste%2A>、<xref:System.Windows.Input.ApplicationCommands.Copy%2A>、<xref:System.Windows.Input.ApplicationCommands.Cut%2A>、<xref:System.Windows.Input.ApplicationCommands.Redo%2A> 和 <xref:System.Windows.Input.ApplicationCommands.Undo%2A>。  应用程序开发人员不必执行任何特殊的操作即可使这些命令适用于这些控件。  如果 <xref:System.Windows.Controls.TextBox> 是执行命令的命令目标，则此控件将使用其内置的 <xref:System.Windows.Input.CommandBinding> 来处理该命令。  
  
 下面演示如何将 <xref:System.Windows.Controls.Button> 用作 <xref:System.Windows.Input.ApplicationCommands.Open%2A> 命令的命令源。  创建 <xref:System.Windows.Input.CommandBinding>，并使用 <xref:System.Windows.Input.RoutedCommand> 将它与指定的 <xref:System.Windows.Input.CanExecuteRoutedEventHandler> 和 <xref:System.Windows.Input.CanExecuteRoutedEventHandler> 关联。  
  
 首先创建命令源。  <xref:System.Windows.Controls.Button> 用作命令源。  
  
 [!code-xml[commandWithHandler#CommandHandlerCommandSource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml#commandhandlercommandsource)]  
  
 [!code-csharp[CommandHandlerProcedural#CommandHandlerButtonCommandSource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandHandlerProcedural/CSharp/Window1.xaml.cs#commandhandlerbuttoncommandsource)]
 [!code-vb[CommandHandlerProcedural#CommandHandlerButtonCommandSource](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandHandlerProcedural/visualbasic/window1.xaml.vb#commandhandlerbuttoncommandsource)]  
  
 接着，创建 <xref:System.Windows.Input.ExecutedRoutedEventHandler> 和 <xref:System.Windows.Input.CanExecuteRoutedEventHandler>。  <xref:System.Windows.Input.ExecutedRoutedEventHandler> 只是打开 <xref:System.Windows.MessageBox> 以指出该命令已执行。  <xref:System.Windows.Input.CanExecuteRoutedEventHandler> 将 <xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A> 属性设置为 `true`。  通常，CanExecute 处理程序将执行更彻底的检查，以查看该命令是否可以在当前的命令目标上执行。  
  
 [!code-csharp[commandWithHandler#CommandHandlerBothHandlers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml.cs#commandhandlerbothhandlers)]
 [!code-vb[commandWithHandler#CommandHandlerBothHandlers](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/commandWithHandler/VisualBasic/Window1.xaml.vb#commandhandlerbothhandlers)]  
  
 最后，在应用程序的根 <xref:System.Windows.Window> 上创建 <xref:System.Windows.Input.CommandBinding>，将路由事件处理程序与 <xref:System.Windows.Input.ApplicationCommands.Open%2A> 命令关联。  
  
 [!code-xml[commandWithHandler#CommandHandlerCommandBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml#commandhandlercommandbinding)]  
  
 [!code-csharp[CommandHandlerProcedural#CommandHandlerBindingInit](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandHandlerProcedural/CSharp/Window1.xaml.cs#commandhandlerbindinginit)]
 [!code-vb[CommandHandlerProcedural#CommandHandlerBindingInit](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandHandlerProcedural/visualbasic/window1.xaml.vb#commandhandlerbindinginit)]  
  
## 请参阅  
 [命令概述](../../../../docs/framework/wpf/advanced/commanding-overview.md)   
 [将命令挂钩到支持命令的控件](../../../../docs/framework/wpf/advanced/how-to-hook-up-a-command-to-a-control-with-command-support.md)