---
title: "如何：在 TreeView 中查找 TreeViewItem | Microsoft Docs"
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
  - "TreeView 控件 [WPF], 查找 TreeViewItem"
  - "TreeViewItem [WPF], 查找"
ms.assetid: 72ecd40c-3939-4e01-b617-5e9daa6074d9
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：在 TreeView 中查找 TreeViewItem
<xref:System.Windows.Controls.TreeView> 控件提供了一种用于显示分层数据的便利方法。  如果 <xref:System.Windows.Controls.TreeView> 绑定到数据源，则 <xref:System.Windows.Controls.TreeView.SelectedItem%2A> 属性可为您提供一种用于快速检索所选数据对象的便利方法。  通常最好是使用基础数据对象，但有时您可能需要以编程方式来操作数据的包含 <xref:System.Windows.Controls.TreeViewItem>。  例如，您可能需要以编程方式来扩展 <xref:System.Windows.Controls.TreeViewItem>，或在 <xref:System.Windows.Controls.TreeView> 中选择不同的项。  
  
 若要查找包含特定数据对象的 <xref:System.Windows.Controls.TreeViewItem>，您必须遍历 <xref:System.Windows.Controls.TreeView> 的每个级别。  也可对 <xref:System.Windows.Controls.TreeView> 中的项进行虚拟化以提高性能。  在可能要对各项进行虚拟化的情况下，还必须要实现 <xref:System.Windows.Controls.TreeViewItem> 以检查其是否包含数据对象。  
  
## 示例  
  
## 说明  
 下面的示例在 <xref:System.Windows.Controls.TreeView> 中搜索特定对象，并返回该对象的包含 <xref:System.Windows.Controls.TreeViewItem>。  该示例确保对每个 <xref:System.Windows.Controls.TreeViewItem> 进行实例化，以便可以搜索其子项。  此示例也适用于 <xref:System.Windows.Controls.TreeView> 不使用虚拟化项的情况。  
  
> [!NOTE]
>  下面的示例适用于任何 <xref:System.Windows.Controls.TreeView>（与基础数据模型无关），并会搜索每个 <xref:System.Windows.Controls.TreeViewItem>，直到找到对象。  具有更佳性能的另一种方法是在数据模型中搜索指定对象，跟踪该对象在数据层次结构中的位置，然后在 <xref:System.Windows.Controls.TreeView> 中查找相应 <xref:System.Windows.Controls.TreeViewItem>。  但是，使用性能更佳的方法需具有数据模型的知识，并且不能通用于任何给定 <xref:System.Windows.Controls.TreeView>。  
  
## 代码  
 [!code-csharp[TreeViewFindTVI#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml.cs#1)]
 [!code-vb[TreeViewFindTVI#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TreeViewFindTVI/VisualBasic/MainWindow.xaml.vb#1)]  
  
 上面的代码依赖于公开名为 `BringIntoView` 的方法的自定义 <xref:System.Windows.Controls.VirtualizingStackPanel>。  下面的代码定义自定义 <xref:System.Windows.Controls.VirtualizingStackPanel>。  
  
 [!code-csharp[TreeViewFindTVI#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml.cs#2)]
 [!code-vb[TreeViewFindTVI#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TreeViewFindTVI/VisualBasic/MainWindow.xaml.vb#2)]  
  
 下面的 XAML 演示如何创建使用自定义 <xref:System.Windows.Controls.VirtualizingStackPanel> 的 <xref:System.Windows.Controls.TreeView>。  
  
 [!code-xml[TreeViewFindTVI#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml#3)]  
  
## 请参阅  
 [提高 TreeView 的性能](../../../../docs/framework/wpf/controls/how-to-improve-the-performance-of-a-treeview.md)