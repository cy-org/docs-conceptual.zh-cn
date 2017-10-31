---
title: "ListView 概述 | Microsoft Docs"
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
  - "控件, ListView"
  - "ListView 控件 [WPF], 关于 ListView 控件"
ms.assetid: 989e12b0-260e-4570-95c6-489284003ce2
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# ListView 概述
<xref:System.Windows.Controls.ListView> 控件提供了一个基础结构，用于在不同的布局或视图中显示一组数据项。  例如，用户可能需要在表中显示数据项，并同时对表的列进行排序。  
  
   
  
<a name="WhatisaListView"></a>   
## 什么是 ListView？  
 <xref:System.Windows.Controls.ListView> 控件是一种从 <xref:System.Windows.Controls.ListBox> 派生而来的 <xref:System.Windows.Controls.ItemsControl>。  通常，该控件的项是数据集合的成员，并且表示为 <xref:System.Windows.Controls.ListViewItem> 对象。  <xref:System.Windows.Controls.ListViewItem> 是一种 <xref:System.Windows.Controls.ContentControl>，并且只能包含单一子元素。  但是，该子元素可以是任何可视元素。  
  
<a name="DefiningaListViewView"></a>   
## 为 ListView 定义视图模式  
 若要为 <xref:System.Windows.Controls.ListView> 控件的内容指定视图模式，请设置 <xref:System.Windows.Controls.ListView.View%2A> 属性。  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供的一个视图模式是 <xref:System.Windows.Controls.GridView>，该模式在具有可自定义的列的表中显示数据项集合。  
  
 下面的示例演示如何为显示雇员信息的 <xref:System.Windows.Controls.ListView> 控件定义 <xref:System.Windows.Controls.GridView>。  
  
 [!code-xml[ListViewCode#ListViewEmployee](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 下图演示了前面示例的数据显示方式。  
  
 ![具有 GridView 输出的 ListView](../../../../docs/framework/wpf/controls/media/listviewgridview.png "ListViewGridView")  
  
 您可以通过定义一个从 <xref:System.Windows.Controls.ViewBase> 类继承的类来创建自定义视图模式。  <xref:System.Windows.Controls.ViewBase> 类提供了创建自定义视图所需的基础结构。  有关如何创建自定义视图的更多信息，请参见[为 ListView 创建自定义视图模式](../../../../docs/framework/wpf/controls/how-to-create-a-custom-view-mode-for-a-listview.md)。  
  
<a name="BindingDatatoaListView"></a>   
## 将数据绑定到 ListView  
 使用 <xref:System.Windows.Controls.ItemsControl.Items%2A> 和 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性为 <xref:System.Windows.Controls.ListView> 控件指定项。  下面的示例将 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性设置为一个名为 `EmployeeInfoDataSource` 的数据集合。  
  
 [!code-xml[ListViewCode#ItemsSource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#itemssource)]  
  
 在 <xref:System.Windows.Controls.GridView> 中，<xref:System.Windows.Controls.GridViewColumn> 对象绑定到指定的数据字段。  下面的示例通过为 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 属性指定 <xref:System.Windows.Data.Binding>，将 <xref:System.Windows.Controls.GridViewColumn> 对象绑定到数据字段。  
  
 [!code-csharp[ListViewCode#GridViewColumnProperties](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml.cs#gridviewcolumnproperties)]
 [!code-vb[ListViewCode#GridViewColumnProperties](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCode/visualbasic/window1.xaml.vb#gridviewcolumnproperties)]
 [!code-xml[ListViewCode#GridViewColumnProperties](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#gridviewcolumnproperties)]  
  
 您也可以指定 <xref:System.Windows.Data.Binding> 作为 <xref:System.Windows.DataTemplate> 用于为列中的单元格设置样式的定义的一部分。  在下面的示例中，用 <xref:System.Windows.ResourceKey> 标识的 <xref:System.Windows.DataTemplate> 为 <xref:System.Windows.Controls.GridViewColumn> 设置 <xref:System.Windows.Data.Binding>。  请注意，此示例未定义 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A>，因为这样做将覆盖 <xref:System.Windows.DataTemplate> 指定的绑定。  
  
 [!code-xml[ListViewTemplate#GridViewCellTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcelltemplate)]  
  
 [!code-xml[ListViewTemplate#CellTemplateProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#celltemplateproperty)]  
  
<a name="StylingaListView"></a>   
## 为实现 GridView 的 ListView 设置样式  
 <xref:System.Windows.Controls.ListView> 控件包含 <xref:System.Windows.Controls.ListViewItem> 对象，这些对象代表显示的数据项。  您可以使用以下属性来定义数据项的内容和样式：  
  
-   在 <xref:System.Windows.Controls.ListView> 控件上，使用 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>、<xref:System.Windows.Controls.ItemsControl.ItemTemplateSelector%2A> 和 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 属性。  
  
-   在 <xref:System.Windows.Controls.ListViewItem> 控件上，使用 <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> 和 <xref:System.Windows.Controls.ContentControl.ContentTemplateSelector%2A> 属性。  
  
 为了避免 <xref:System.Windows.Controls.GridView> 中的单元格之间出现对齐问题，请不要使用 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 来设置属性，或添加对 <xref:System.Windows.Controls.ListView> 中项的宽度有影响的内容。  例如，如果在 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 中设置 <xref:System.Windows.FrameworkElement.Margin%2A> 属性，则可能会出现对齐问题。  若要指定属性或定义对 <xref:System.Windows.Controls.GridView> 中项的宽度有影响的内容，请使用 <xref:System.Windows.Controls.GridView> 类及其相关类（如 <xref:System.Windows.Controls.GridViewColumn>）的属性。  
  
 有关如何使用 <xref:System.Windows.Controls.GridView> 及其支持类的更多信息，请参见 [GridView 概述](../../../../docs/framework/wpf/controls/gridview-overview.md)。  
  
 如果为 <xref:System.Windows.Controls.ListView> 控件定义 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 并同时定义 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>，您必须在样式中包括 <xref:System.Windows.Controls.ContentPresenter> 才能使 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 正常工作。  
  
 不要为通过使用 <xref:System.Windows.Controls.GridView> 显示的 <xref:System.Windows.Controls.ListView> 内容使用 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> 和 <xref:System.Windows.Controls.Control.VerticalContentAlignment%2A> 属性。  若要指定 <xref:System.Windows.Controls.GridView> 的列中内容的对齐方式，请定义 <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A>。  
  
<a name="UsingtheSameViewMoreThanOnce"></a>   
## 共用同一视图模式  
 两个 <xref:System.Windows.Controls.ListView> 控件不能同时共用同一个视图模式。  如果尝试将同一视图模式用于多个 <xref:System.Windows.Controls.ListView> 控件，则会出现异常。  
  
 若要指定可同时由多个 <xref:System.Windows.Controls.ListView> 使用的视图模式，请使用模板或样式。  有关如何将视图定义为 <xref:System.Windows.FrameworkElement.Resources%2A> 的示例，请参见 [ListView with Multiple Views Sample](http://go.microsoft.com/fwlink/?LinkID=160013)（具有多个视图的 ListView 示例）。  
  
<a name="CreatingaCustomView"></a>   
## 创建自定义视图模式  
 诸如 <xref:System.Windows.Controls.GridView> 的自定义视图派生自 <xref:System.Windows.Controls.ViewBase> 抽象类，该类提供了一些工具，用于显示表示为 <xref:System.Windows.Controls.ListViewItem> 对象的数据项。  
  
 有关自定义视图模式的示例，请参见 [ListView with Multiple Views Sample](http://go.microsoft.com/fwlink/?LinkID=160013)（具有多个视图的 ListView 示例）。  
  
## 请参阅  
 <xref:System.Windows.Controls.GridView>   
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.ListViewItem>   
 <xref:System.Windows.Data.Binding>   
 [GridView 概述](../../../../docs/framework/wpf/controls/gridview-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [控件](../../../../docs/framework/wpf/advanced/optimizing-performance-controls.md)