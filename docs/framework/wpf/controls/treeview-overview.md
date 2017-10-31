---
title: "TreeView 概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Control 类, TreeView"
  - "展开节点"
  - "TreeView 控件, 关于 TreeView 控件"
ms.assetid: 62212512-5a5c-4864-949e-b6a6a3a52c02
caps.latest.revision: 33
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 32
---
# TreeView 概述
<xref:System.Windows.Controls.TreeView> 控件通过使用可折叠节点提供一种以分层结构来显示信息的方式。  本主题介绍 <xref:System.Windows.Controls.TreeView> 和 <xref:System.Windows.Controls.TreeViewItem> 控件，并提供了其用法的简单示例。  
  
   
  
<a name="Simple_TreeView_Control"></a>   
## 什么是 TreeView  
 <xref:System.Windows.Controls.TreeView> 是一个使用 <xref:System.Windows.Controls.TreeViewItem> 控件来嵌套项的 <xref:System.Windows.Controls.ItemsControl>。  下面的示例创建一个 <xref:System.Windows.Controls.TreeView>。  
  
 [!code-xml[TreeViewSnips#EmbeddedTVIs](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSnips/CSharp/Window1.xaml#embeddedtvis)]  
  
<a name="Creating_a_TreeView"></a>   
## 创建 TreeView  
 <xref:System.Windows.Controls.TreeView> 控件包含 <xref:System.Windows.Controls.TreeViewItem> 控件的层次结构。  <xref:System.Windows.Controls.TreeViewItem> 控件是一个具有 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 和 <xref:System.Windows.Controls.ItemsControl.Items%2A> 集合的 <xref:System.Windows.Controls.HeaderedItemsControl>。  
  
 如果使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 定义 <xref:System.Windows.Controls.TreeView>，那么可以显式定义 <xref:System.Windows.Controls.TreeViewItem> 控件的 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 内容以及构成其集合的项。  上图演示了此方法。  
  
 还可以指定 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 作为数据源，然后指定 <xref:System.Windows.Controls.HeaderedItemsControl.HeaderTemplate%2A> 和 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 以定义 <xref:System.Windows.Controls.TreeViewItem> 内容。  
  
 若要定义 <xref:System.Windows.Controls.TreeViewItem> 控件的布局，还可以使用 <xref:System.Windows.HierarchicalDataTemplate> 对象。  有关更多信息及示例，请参见[使用 SelectedValue、SelectedValuePath 和 SelectedItem](../../../../docs/framework/wpf/controls/how-to-use-selectedvalue-selectedvaluepath-and-selecteditem.md)。  
  
 如果某项不是 <xref:System.Windows.Controls.TreeViewItem> 控件，那么在显示 <xref:System.Windows.Controls.TreeView> 控件时，<xref:System.Windows.Controls.TreeViewItem> 控件将自动包括此项。  
  
<a name="Expanding_and_Collapsing_a_TreeViewItem"></a>   
## 展开和折叠 TreeViewItem  
 如果用户展开 <xref:System.Windows.Controls.TreeViewItem>，则 <xref:System.Windows.Controls.TreeViewItem.IsExpanded%2A> 属性设置为 `true`。  还可以通过将 <xref:System.Windows.Controls.TreeViewItem.IsExpanded%2A> 属性设置为 `true`（展开）或 `false`（折叠）来展开或折叠 <xref:System.Windows.Controls.TreeViewItem>，而无需直接进行任何用户操作。  当该属性更改时，将发生 <xref:System.Windows.Controls.TreeViewItem.Expanded> 或 <xref:System.Windows.Controls.TreeViewItem.Collapsed> 事件。  
  
 对 <xref:System.Windows.Controls.TreeViewItem> 控件调用 <xref:System.Windows.FrameworkElement.BringIntoView%2A> 方法时，<xref:System.Windows.Controls.TreeViewItem> 及其父级 <xref:System.Windows.Controls.TreeViewItem> 控件将展开。  如果 <xref:System.Windows.Controls.TreeViewItem> 不可见或部分可见，则 <xref:System.Windows.Controls.TreeView> 将滚动以使其可见。  
  
<a name="TreeViewItem_Selection"></a>   
## TreeViewItem 选择  
 当用户单击 <xref:System.Windows.Controls.TreeViewItem> 控件以选择该控件时，将发生 <xref:System.Windows.Controls.TreeViewItem.Selected> 事件，且其 <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> 属性设置为 `true`。  <xref:System.Windows.Controls.TreeViewItem> 还会成为 <xref:System.Windows.Controls.TreeView> 控件的 <xref:System.Windows.Controls.TreeView.SelectedItem%2A>。  相反，当所选内容从 <xref:System.Windows.Controls.TreeViewItem> 控件变为其他内容时，将发生其 <xref:System.Windows.Controls.TreeViewItem.Unselected> 事件，且其 <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> 属性设置为 `false`。  
  
 <xref:System.Windows.Controls.TreeView> 控件上的 <xref:System.Windows.Controls.TreeView.SelectedItem%2A> 属性为只读属性，因此无法显式设置。  当用户单击 <xref:System.Windows.Controls.TreeViewItem> 控件，或 <xref:System.Windows.Controls.TreeViewItem> 控件上的 <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> 属性设置为 `true` 时，将设置 <xref:System.Windows.Controls.TreeView.SelectedItem%2A> 属性。  
  
 使用 <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> 属性指定 <xref:System.Windows.Controls.TreeView.SelectedItem%2A> 的 <xref:System.Windows.Controls.TreeView.SelectedValue%2A>。  有关更多信息，请参见[使用 SelectedValue、SelectedValuePath 和 SelectedItem](../../../../docs/framework/wpf/controls/how-to-use-selectedvalue-selectedvaluepath-and-selecteditem.md)。  
  
 可以对 <xref:System.Windows.Controls.TreeView.SelectedItemChanged> 事件注册事件处理程序，以确定选定的 <xref:System.Windows.Controls.TreeViewItem> 何时发生变化。  为事件处理程序提供的 <xref:System.Windows.RoutedPropertyChangedEventArgs%601> 指定 <xref:System.Windows.RoutedPropertyChangedEventArgs%601.OldValue%2A>（上一个选择）和 <xref:System.Windows.RoutedPropertyChangedEventArgs%601.NewValue%2A>（当前选择）。  如果应用程序或用户未做出上一个选择或当前选择，则这两个值都可能为 `null`。  
  
<a name="TreeView_Style"></a>   
## TreeView 样式  
 <xref:System.Windows.Controls.TreeView> 控件的默认样式是将其放在包含 <xref:System.Windows.Controls.ScrollViewer> 控件的 <xref:System.Windows.Controls.StackPanel> 对象内。  在为 <xref:System.Windows.Controls.TreeView> 设置 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性时，这些值用于确定显示 <xref:System.Windows.Controls.TreeView> 的 <xref:System.Windows.Controls.StackPanel> 对象的大小。  如果要显示的内容大于显示区域，将自动显示 <xref:System.Windows.Controls.ScrollViewer>，以便用户能滚动查看 <xref:System.Windows.Controls.TreeView> 内容。  
  
 若要自定义 <xref:System.Windows.Controls.TreeViewItem> 控件的外观，请将 <xref:System.Windows.FrameworkElement.Style%2A> 属性设置为自定义 <xref:System.Windows.Style>。  
  
 下面的示例演示如何使用 <xref:System.Windows.FrameworkElement.Style%2A> 为 <xref:System.Windows.Controls.TreeViewItem> 控件设置 <xref:System.Windows.Controls.Control.Foreground%2A> 和 <xref:System.Windows.Controls.Control.FontSize%2A> 属性值。  
  
 [!code-xml[TreeViewSimple#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#8)]  
  
<a name="Adding_Images_and_oOther_Content_to_TreeView_Items"></a>   
## 向 TreeView 项中添加图像和其他内容  
 可以在 <xref:System.Windows.Controls.TreeViewItem> 的 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 内容中包括多个对象。  若要在 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 内容中包括多个对象，请将这些对象包含在布局控件内，如 <xref:System.Windows.Controls.Panel> 或 <xref:System.Windows.Controls.StackPanel>。  
  
 下面的示例演示如何将 <xref:System.Windows.Controls.TreeViewItem> 的 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 定义为 <xref:System.Windows.Controls.CheckBox> 和 <xref:System.Windows.Controls.TextBlock>，二者均包括在 <xref:System.Windows.Controls.DockPanel> 控件中。  
  
 [!code-xml[TreeViewSnips#TVIHeader](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSnips/CSharp/Window1.xaml#tviheader)]  
  
 下面的示例演示如何定义包含 <xref:System.Windows.Controls.Image> 和 <xref:System.Windows.Controls.TextBlock> 的 <xref:System.Windows.DataTemplate>，这两个对象均包含在 <xref:System.Windows.Controls.DockPanel> 控件中。  可以使用 <xref:System.Windows.DataTemplate> 为 <xref:System.Windows.Controls.TreeViewItem> 设置 <xref:System.Windows.Controls.HeaderedItemsControl.HeaderTemplate%2A> 或 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>。  
  
 [!code-xml[TreeViewDataBinding#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewDataBinding/CSharp/Window1.xaml#6)]  
  
## 请参阅  
 <xref:System.Windows.Controls.TreeView>   
 <xref:System.Windows.Controls.TreeViewItem>   
 [帮助主题](../../../../docs/framework/wpf/controls/treeview-how-to-topics.md)   
 [WPF 内容模型](../../../../docs/framework/wpf/controls/wpf-content-model.md)