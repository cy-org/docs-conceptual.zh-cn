---
title: "如何：将命令挂钩到支持命令的控件 | Microsoft Docs"
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
  - "控件类中，附加 RoutedCommand"
  - "类、 控件，附加 RoutedCommand"
  - "RoutedCommand 类中，将附加到控件"
  - "类，RoutedCommand，附加到 Control"
ms.assetid: 8d8592ae-0c91-469e-a1cd-d179c4544548
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：将命令挂钩到支持命令的控件
下面的示例演示如何挂接<xref:System.Windows.Input.RoutedCommand>到<xref:System.Windows.Controls.Control>提供了内置命令的支持。  它挂接到多个源的命令的完整示例，请参阅[创建自定义 RoutedCommand 示例](http://go.microsoft.com/fwlink/?LinkID=159980)示例。  
  
## <a name="example"></a>示例  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]提供一个库应用程序程序员经常遇到的常见命令。  构成命令库类，这些类是︰ <xref:System.Windows.Input.ApplicationCommands>， <xref:System.Windows.Input.ComponentCommands>， <xref:System.Windows.Input.NavigationCommands>， <xref:System.Windows.Input.MediaCommands>，和<xref:System.Windows.Documents.EditingCommands>。  
  
 静态<xref:System.Windows.Input.RoutedCommand>构成这些类的对象不提供命令逻辑。  该命令的逻辑是与命令相关联<xref:System.Windows.Input.CommandBinding>。  某些命令的情况下，某些控件具有内置的 CommandBindings。  此机制允许的语义保持不变，而实际的实现是一个命令可以更改。  一个<xref:System.Windows.Controls.TextBox>，例如，将处理<xref:System.Windows.Input.ApplicationCommands.Paste%2A>命令以不同的方式不是控件设计为支持图像，但这意味着粘贴操作的基本思想保持不变。  命令逻辑不能提供的命令，但而是必须提供由该控件或应用程序。  
  
 中的许多控件[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]执行具有内置的对某些命令库中的命令的支持。  <xref:System.Windows.Controls.TextBox>，例如，如支持的许多应用程序编辑命令<xref:System.Windows.Input.ApplicationCommands.Paste%2A>，<xref:System.Windows.Input.ApplicationCommands.Copy%2A>，<xref:System.Windows.Input.ApplicationCommands.Cut%2A>，<xref:System.Windows.Input.ApplicationCommands.Redo%2A>，和<xref:System.Windows.Input.ApplicationCommands.Undo%2A>。  应用程序开发人员不需要执行任何特殊即可将这些命令，以使用这些控件。  如果<xref:System.Windows.Controls.TextBox>是命令目标执行该命令时，它将处理命令使用<xref:System.Windows.Input.CommandBinding>内置控件。  
  
 以下示例显示如何使用<xref:System.Windows.Controls.MenuItem>作为命令源<xref:System.Windows.Input.ApplicationCommands.Paste%2A>命令，其中<xref:System.Windows.Controls.TextBox>是命令目标。  定义的所有逻辑如何<xref:System.Windows.Controls.TextBox>执行粘贴内置于<xref:System.Windows.Controls.TextBox>控件。  
  
 一个<xref:System.Windows.Controls.MenuItem>创建，且<xref:System.Windows.Controls.MenuItem.Command%2A>属性设置为<xref:System.Windows.Input.ApplicationCommands.Paste%2A>命令。  <xref:System.Windows.Controls.MenuItem.CommandTarget%2A>未显式设置为<xref:System.Windows.Controls.TextBox>对象。  当<xref:System.Windows.Controls.MenuItem.CommandTarget%2A>未设置，则目标中的命令为具有键盘焦点的元素。  如果将具有键盘焦点的元素不支持<xref:System.Windows.Input.ApplicationCommands.Paste%2A>命令或者目前无法执行粘贴命令 （剪贴板是空的例如） 则<xref:System.Windows.Controls.MenuItem>将灰显。  
  
 [!code-xml[MenuItemCommandTask_XAML#MenuItemCommanding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandTask_XAML/CS/Window1.xaml#menuitemcommanding)]  
  
 [!code-csharp[MenuItemCommandTask#MenuItemCommandingCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandTask/CSharp/Window1.xaml.cs#menuitemcommandingcodebehind)]
 [!code-vb[MenuItemCommandTask#MenuItemCommandingCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MenuItemCommandTask/VisualBasic/Window1.xaml.vb#menuitemcommandingcodebehind)]  
  
## <a name="see-also"></a>另请参阅  
 [命令概述](../../../../docs/framework/wpf/advanced/commanding-overview.md)   
 [到不支持命令的控件将命令挂钩](../../../../docs/framework/wpf/advanced/how-to-hook-up-a-command-to-a-control-with-no-command-support.md)