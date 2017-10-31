---
title: "如何：提高 TreeView 的性能 | Microsoft Docs"
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
  - "TreeView 控件 [WPF], 提高性能"
ms.assetid: b792c740-cf2b-4da8-8ba8-3d2e5a821874
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：提高 TreeView 的性能
如果 <xref:System.Windows.Controls.TreeView> 包含很多项，则加载所用的时间可能导致用户界面的明显延迟。  可以通过将 <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A?displayProperty=fullName> 附加属性设置为 `true` 来缩短加载时间。  当用户通过使用鼠标滚轮或拖动滚动条上的滚动块来滚动 <xref:System.Windows.Controls.TreeView> 时，用户界面可能也会反应迟缓。  可以通过将 <xref:System.Windows.Controls.VirtualizingStackPanel.VirtualizationMode%2A?displayProperty=fullName> 附加属性设置为 <xref:System.Windows.Controls.VirtualizationMode>，提高 <xref:System.Windows.Controls.TreeView> 在用户滚动时的性能。  
  
## 示例  
  
## 说明  
 下面的示例创建一个 <xref:System.Windows.Controls.TreeView>，它将 <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A?displayProperty=fullName> 设置为 True，将 <xref:System.Windows.Controls.VirtualizingStackPanel.VirtualizationMode%2A?displayProperty=fullName> 设置为 <xref:System.Windows.Controls.VirtualizationMode> 以优化其性能。  
  
## 代码  
 [!code-xml[RecycleItemContainerShippets#VirtualizingTreeView](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml#virtualizingtreeview)]  
  
 下面的示例显示上例所使用的数据。  
  
 [!code-csharp[RecycleItemContainerShippets#TreeViewData](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml.cs#treeviewdata)]
 [!code-vb[RecycleItemContainerShippets#TreeViewData](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RecycleItemContainerShippets/visualbasic/window1.xaml.vb#treeviewdata)]  
  
## 请参阅  
 [控件](../../../../docs/framework/wpf/advanced/optimizing-performance-controls.md)