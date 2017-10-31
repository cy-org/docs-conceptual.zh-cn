---
title: "如何：使用 SelectedValue、SelectedValuePath 和 SelectedItem | Microsoft Docs"
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
  - "Control 类, SelectedItem 属性"
  - "Control 类, SelectedValue 属性"
  - "Control 类, SelectedValuePath 属性"
  - "Control 类, TreeView 属性"
  - "SelectedValue, SelectedItem 属性"
  - "SelectedValue, SelectedValuePath 属性"
  - "TreeView 控件, SelectedItem 属性"
  - "TreeView 控件, SelectedValue 属性"
  - "TreeView 控件, SelectedValuePath 属性"
ms.assetid: 2fc92ad4-f02c-4f89-bbe9-d4978a7af0db
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用 SelectedValue、SelectedValuePath 和 SelectedItem
此示例演示如何使用 <xref:System.Windows.Controls.TreeView.SelectedValue%2A> 和 <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> 属性为 <xref:System.Windows.Controls.TreeView> 的 <xref:System.Windows.Controls.TreeView.SelectedItem%2A> 指定值。  
  
## 示例  
 <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> 属性提供了一种为 <xref:System.Windows.Controls.TreeView> 中的 <xref:System.Windows.Controls.TreeView.SelectedItem%2A> 指定 <xref:System.Windows.Controls.TreeView.SelectedValue%2A> 的方法。  <xref:System.Windows.Controls.TreeView.SelectedItem%2A> 表示 <xref:System.Windows.Controls.ItemsControl.Items%2A> 集合中的对象，<xref:System.Windows.Controls.TreeView> 显示选定项的单个属性的值。  <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> 属性指定用于确定 <xref:System.Windows.Controls.TreeView.SelectedValue%2A> 属性的值的属性的路径。  本主题中的示例阐释了这一概念。  
  
 下面的示例演示包含雇员信息的 <xref:System.Windows.Data.XmlDataProvider>。  
  
 [!code-xml[TreeViewSelectedValue#XMLDataProvider](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSelectedValue/CS/Window1.xaml#xmldataprovider)]  
  
 下面的示例定义用于显示 `Employee` 的 `EmployeeName` 和 `EmployeeWorkDay` 的 <xref:System.Windows.HierarchicalDataTemplate>。  请注意 <xref:System.Windows.HierarchicalDataTemplate> 不会将 `EmployeeNumber` 指定为模板的一部分。  
  
 [!code-xml[TreeViewSelectedValue#HierarchicalDataTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSelectedValue/CS/Window1.xaml#hierarchicaldatatemplate)]  
  
 下面的示例演示 <xref:System.Windows.Controls.TreeView>，它使用之前定义的 <xref:System.Windows.HierarchicalDataTemplate>，并将 <xref:System.Windows.Controls.TreeView.SelectedValue%2A> 属性设置为 `EmployeeNumber`。  当您在 <xref:System.Windows.Controls.TreeView> 中选择 `EmployeeName` 时，<xref:System.Windows.Controls.TreeView.SelectedItem%2A> 属性将返回与选定的 `EmployeeName` 对应的 `EmployeeInfo` 数据项。  但是，由于此 <xref:System.Windows.Controls.TreeView> 的 <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> 被设置为 `EmployeeNumber`，因此 <xref:System.Windows.Controls.TreeView.SelectedValue%2A> 也被设置为 `EmployeeNumber`。  
  
 [!code-xml[TreeViewSelectedValue#SelectedValuePath](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSelectedValue/CS/Window1.xaml#selectedvaluepath)]  
  
## 请参阅  
 <xref:System.Windows.Controls.TreeView>   
 <xref:System.Windows.Controls.TreeViewItem>   
 [TreeView 概述](../../../../docs/framework/wpf/controls/treeview-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/treeview-how-to-topics.md)