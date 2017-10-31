---
title: "如何：实现 ICommandSource | Microsoft Docs"
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
  - "ICommandSource 接口, 实现"
  - "接口, ICommandSource, 实现"
ms.assetid: 7452dd39-6e11-44bf-806a-31d87f3772ac
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：实现 ICommandSource
本示例演示如何通过实现 <xref:System.Windows.Input.ICommandSource> 来创建命令源。  命令源是一个知道如何调用命令的对象。  <xref:System.Windows.Input.ICommandSource> 接口公开三个成员：<xref:System.Windows.Input.ICommandSource.Command%2A>、<xref:System.Windows.Input.ICommandSource.CommandParameter%2A> 和 <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>。  <xref:System.Windows.Input.ICommandSource.Command%2A> 是将调用的命令。  <xref:System.Windows.Input.ICommandSource.CommandParameter%2A> 是用户定义的数据类型，它从命令源传递到处理命令的方法。  <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> 是命令所作用于的对象。  
  
 在本示例中，创建这样一个类：它是 <xref:System.Windows.Controls.Slider> 控件的子类并实现 <xref:System.Windows.Input.ICommandSource>。  
  
## 示例  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供许多实现 <xref:System.Windows.Input.ICommandSource> 的类，如 <xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.MenuItem> 和 <xref:System.Windows.Controls.ListBoxItem>。  命令源定义其调用命令的方式。  单击 <xref:System.Windows.Controls.Button> 和 <xref:System.Windows.Controls.MenuItem> 时，它们就会调用命令。  <xref:System.Windows.Controls.ListBoxItem> 在被双击时调用一个命令。  这些类只有在设置了 <xref:System.Windows.Input.ICommandSource.Command%2A> 属性时才会成为命令源。  
  
 对于本示例，我们将在滑块移动时调用命令，更准确地说，是在 <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> 属性更改时调用命令。  
  
 类定义如下。  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceClassDefinition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourceclassdefinition)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceClassDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourceclassdefinition)]  
  
 下一步是实现 <xref:System.Windows.Input.ICommandSource> 成员。  在本示例中，属性实现为 <xref:System.Windows.DependencyProperty> 对象。  这使属性可以使用数据绑定。  有关 <xref:System.Windows.DependencyProperty> 类的更多信息，请参见[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  有关数据绑定的更多信息，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
 这里只显示 <xref:System.Windows.Input.ICommandSource.Command%2A> 属性。  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceCommandPropertyDefinition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcecommandpropertydefinition)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceCommandPropertyDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcecommandpropertydefinition)]  
  
 下面是 <xref:System.Windows.DependencyProperty> 更改回调。  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceCommandChanged](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcecommandchanged)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceCommandChanged](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcecommandchanged)]  
  
 下一步是添加和移除与命令源关联的命令。  在添加新命令时，不能简单地改写 <xref:System.Windows.Input.ICommandSource.Command%2A> 属性，因为必须先移除与前一个命令关联的事件处理程序（如果有的话）。  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceHookUnHookCommands](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcehookunhookcommands)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceHookUnHookCommands](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcehookunhookcommands)]  
  
 最后一步是为 <xref:System.Windows.Input.ICommand.CanExecuteChanged> 处理程序和 <xref:System.Windows.Input.ICommand.Execute%2A> 方法创建逻辑。  
  
 <xref:System.Windows.Input.ICommand.CanExecuteChanged> 事件通知命令源，在当前命令目标上执行命令的能力可能已更改。  当命令源接收到此事件时，通常会对命令调用 <xref:System.Windows.Input.ICommand.CanExecute%2A> 方法。  如果命令无法在当前命令目标上执行，那么命令源通常会禁用自身。  如果命令可以在当前命令目标上执行，那么命令源通常会启用自身。  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandCanExecuteChanged](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandcanexecutechanged)]
 [!code-vb[ImplementICommandSource#ImplementICommandCanExecuteChanged](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandcanexecutechanged)]  
  
 最后一步是 <xref:System.Windows.Input.ICommand.Execute%2A> 方法。  如果命令是 <xref:System.Windows.Input.RoutedCommand>，则会调用 <xref:System.Windows.Input.RoutedCommand> <xref:System.Windows.Input.RoutedCommand.Execute%2A> 方法；否则会调用 <xref:System.Windows.Input.ICommand> <xref:System.Windows.Input.ICommand.Execute%2A> 方法。  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandExecute](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandexecute)]
 [!code-vb[ImplementICommandSource#ImplementICommandExecute](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandexecute)]  
  
## 请参阅  
 <xref:System.Windows.Input.ICommandSource>   
 <xref:System.Windows.Input.ICommand>   
 <xref:System.Windows.Input.RoutedCommand>   
 [命令概述](../../../../docs/framework/wpf/advanced/commanding-overview.md)