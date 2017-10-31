---
title: "如何：创建简单或复杂的 TreeView | Microsoft Docs"
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
  - "Control 类, TreeView, 创建"
  - "TreeView 控件, 创建"
ms.assetid: 1defbb78-b8e7-4c0e-b650-576453ac828d
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：创建简单或复杂的 TreeView
此示例演示如何创建简单或复杂的 <xref:System.Windows.Controls.TreeView> 控件。  
  
 <xref:System.Windows.Controls.TreeView> 由一个层次结构组成，该层次结构中包含多个 <xref:System.Windows.Controls.TreeViewItem> 控件，这些控件可以包含简单的文本字符串，还可以包含更为复杂的内容（如 <xref:System.Windows.Controls.Button> 控件或具有嵌入内容的 <xref:System.Windows.Controls.StackPanel>）。  <xref:System.Windows.Controls.TreeView> 内容可以由您显式定义，也可以由数据源提供。  本主题提供这些概念的示例。  
  
## 示例  
 <xref:System.Windows.Controls.TreeViewItem> 的 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 属性包含 <xref:System.Windows.Controls.TreeView> 针对该项显示的内容。  <xref:System.Windows.Controls.TreeViewItem> 还可以将 <xref:System.Windows.Controls.TreeViewItem> 控件用作其子元素，这些子元素可以通过使用 <xref:System.Windows.Controls.ItemsControl.Items%2A> 属性来定义。  
  
 下面的示例演示如何通过将 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 属性设置为文本字符串来显式定义 <xref:System.Windows.Controls.TreeViewItem> 内容。  
  
 [!code-xml[TreeViewSimple#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#1)]  
  
 下面的示例演示如何通过定义作为 <xref:System.Windows.Controls.Button> 控件的 <xref:System.Windows.Controls.ItemsControl.Items%2A> 来定义 <xref:System.Windows.Controls.TreeViewItem> 的子元素。  
  
 [!code-xml[TreeViewSimple#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#3)]  
  
 下面的示例演示如何 <xref:System.Windows.Controls.TreeView>，其中的 <xref:System.Windows.Data.XmlDataProvider> 提供 <xref:System.Windows.Controls.TreeViewItem> 内容，<xref:System.Windows.HierarchicalDataTemplate> 定义该内容的外观。  
  
 [!code-xml[TreeViewSimple#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#6)]  
  
 [!code-xml[TreeViewSimple#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#7)]  
  
 [!code-xml[TreeViewSimple#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#5)]  
  
 下面的示例演示如何创建 <xref:System.Windows.Controls.TreeView>，其中的 <xref:System.Windows.Controls.TreeViewItem> 内容包含具有嵌入内容的 <xref:System.Windows.Controls.DockPanel> 控件。  
  
 [!code-xml[TreeViewSimple#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#9)]  
  
## 请参阅  
 <xref:System.Windows.Controls.TreeView>   
 <xref:System.Windows.Controls.TreeViewItem>   
 [TreeView 概述](../../../../docs/framework/wpf/controls/treeview-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/treeview-how-to-topics.md)