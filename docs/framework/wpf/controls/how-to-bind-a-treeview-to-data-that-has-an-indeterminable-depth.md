---
title: "如何：将 TreeView 绑定到深度无法确定的数据 | Microsoft Docs"
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
  - "TreeView 控件 [WPF], 绑定到深度不确定的数据"
ms.assetid: daddcd74-1b0f-4ffd-baeb-ec934c5e0f53
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：将 TreeView 绑定到深度无法确定的数据
有时您可能需要将 <xref:System.Windows.Controls.TreeView> 绑定到深度未知的数据源。  如果数据具有递归性质，则可能会发生这种情况；文件系统或公司的组织结构就属于这种数据，在文件系统中，文件夹还可以包含文件夹，在公司的组织结构中，员工又有自己的直属员工。  
  
 数据源必须有分层的对象模型。  例如，一个 `Employee` 类可能包含一个由 Employee 对象组成的集合，其中的每个对象都是一位员工的直属员工。  如果数据以未分层方式表示，则您必须构建该数据的分层表示形式。  
  
 设置 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A?displayProperty=fullName> 属性时，如果 <xref:System.Windows.Controls.ItemsControl> 为每个子项生成了一个 <xref:System.Windows.Controls.ItemsControl>，则子级 <xref:System.Windows.Controls.ItemsControl> 使用同一 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 作为父级。  例如，如果设置绑定到数据的 <xref:System.Windows.Controls.TreeView> 的 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 属性，则所生成的每个 <xref:System.Windows.Controls.TreeViewItem> 都会使用分配给 <xref:System.Windows.Controls.TreeView> 的 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 属性的 <xref:System.Windows.DataTemplate>。  
  
 借助 <xref:System.Windows.HierarchicalDataTemplate>，您可以在数据模板中为 <xref:System.Windows.Controls.TreeViewItem> 或任何 <xref:System.Windows.Controls.HeaderedItemsControl> 指定 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>。  设置 <xref:System.Windows.HierarchicalDataTemplate.ItemsSource%2A?displayProperty=fullName> 属性后，在应用 <xref:System.Windows.HierarchicalDataTemplate> 时会使用该值。  通过使用 <xref:System.Windows.HierarchicalDataTemplate>，您可以以递归方式为 <xref:System.Windows.Controls.TreeView> 中的每个 <xref:System.Windows.Controls.TreeViewItem> 设置 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>。  
  
## 示例  
 下面的示例演示如何将 <xref:System.Windows.Controls.TreeView> 绑定到分层数据并使用 <xref:System.Windows.HierarchicalDataTemplate> 为每个 <xref:System.Windows.Controls.TreeViewItem> 指定 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>。  <xref:System.Windows.Controls.TreeView> 绑定到表示公司内的员工的 XML 数据。  每个 `Employee` 元素可以包含其他 `Employee` 元素，以指示上下级关系。  由于数据是递归的，因此 <xref:System.Windows.HierarchicalDataTemplate> 可应用于每一级。  
  
 [!code-xml[TreeViewWithUnknownDepth#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewWithUnknownDepth/CS/Window1.xaml#1)]  
  
## 请参阅  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)