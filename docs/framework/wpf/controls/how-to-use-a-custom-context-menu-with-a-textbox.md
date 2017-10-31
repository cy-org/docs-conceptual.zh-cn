---
title: "如何：通过 TextBox 使用自定义上下文菜单 | Microsoft Docs"
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
  - "上下文菜单, 自定义"
  - "自定义上下文菜单"
  - "菜单, 自定义"
  - "TextBox 控件, 自定义内容菜单"
ms.assetid: 842d3cd5-6fa0-4be4-8d90-6c7466213b1c
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：通过 TextBox 使用自定义上下文菜单
本示例演示如何为 <xref:System.Windows.Controls.TextBox> 定义和实现一个简单的自定义上下文菜单。  
  
## 示例  
 以下[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 示例定义一个包含自定义上下文菜单的 <xref:System.Windows.Controls.TextBox> 控件。  
  
 该上下文菜单是使用 <xref:System.Windows.Controls.ContextMenu> 元素定义的。  该上下文菜单本身包含一系列 <xref:System.Windows.Controls.MenuItem> 元素和 <xref:System.Windows.Controls.Separator> 元素。  每个 <xref:System.Windows.Controls.MenuItem> 元素都定义上下文菜单中的一个命令，<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 特性定义菜单命令的显示文本，<xref:System.Windows.Controls.MenuItem.Click> 特性指定每个菜单项的处理程序方法。  <xref:System.Windows.Controls.Separator> 元素仅用于在前面的菜单项与后面的菜单项之间呈现一条分隔线。  
  
 [!code-xml[TextBox_ContextMenu#_TextBox_ContextMenuXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_ContextMenu/CSharp/Window1.xaml#_textbox_contextmenuxaml)]  
  
## 示例  
 下面的示例演示前面的上下文菜单定义的实现代码以及启用和禁用上下文菜单的代码。  <xref:System.Windows.Controls.ContextMenu.Opened> 事件用于根据 <xref:System.Windows.Controls.TextBox> 的当前状态动态地启用或禁用某些命令。  
  
 若要还原默认上下文菜单，应使用 <xref:System.Windows.DependencyObject.ClearValue%2A> 方法来清除 <xref:System.Windows.FrameworkElement.ContextMenu%2A> 属性的值。  若要完全禁用上下文菜单，应将 <xref:System.Windows.FrameworkElement.ContextMenu%2A> 属性设置为 null 引用（在 Visual Basic 中为 `Nothing`）。  
  
 [!code-csharp[TextBox_ContextMenu#_TextBox_ContextMenu](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_ContextMenu/CSharp/Window1.xaml.cs#_textbox_contextmenu)]
 [!code-vb[TextBox_ContextMenu#_TextBox_ContextMenu](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_ContextMenu/VisualBasic/Window1.xaml.vb#_textbox_contextmenu)]  
  
## 请参阅  
 [使用上下文菜单中的拼写检查功能](../../../../docs/framework/wpf/controls/how-to-use-spell-checking-with-a-context-menu.md)   
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)