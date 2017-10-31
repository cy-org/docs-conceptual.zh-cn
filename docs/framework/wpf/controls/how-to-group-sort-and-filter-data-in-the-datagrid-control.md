---
title: "如何：在 DataGrid 控件中对数据进行分组、排序和筛选 | Microsoft Docs"
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
  - "DataGrid [WPF], 筛选器"
  - "DataGrid [WPF], 组"
  - "DataGrid [WPF], 排序"
ms.assetid: 03345e85-89e3-4aec-9ed0-3b80759df770
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：在 DataGrid 控件中对数据进行分组、排序和筛选
通过对数据进行分组、排序和筛选，以不同方式查看 <xref:System.Windows.Controls.DataGrid> 中的数据常常很有用。  若要在 <xref:System.Windows.Controls.DataGrid> 中对数据进行分组、排序和筛选，请将其绑定到支持这些功能的 <xref:System.Windows.Data.CollectionView>。  随后便可以在 <xref:System.Windows.Data.CollectionView> 中处理数据，而不会影响基础源数据。  该集合视图中的更改将反映在 <xref:System.Windows.Controls.DataGrid> 用户界面 \(UI\) 中。  
  
 <xref:System.Windows.Data.CollectionView> 类为实现 <xref:System.Collections.IEnumerable> 接口的数据源提供分组和排序功能。  使用 <xref:System.Windows.Data.CollectionViewSource> 类可以从 XAML 设置 <xref:System.Windows.Data.CollectionView> 的属性。  
  
 在此示例中，一个 `Task` 对象集合被绑定到一个 <xref:System.Windows.Data.CollectionViewSource>。  <xref:System.Windows.Data.CollectionViewSource> 用作 <xref:System.Windows.Controls.DataGrid> 的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>。  对 <xref:System.Windows.Data.CollectionViewSource> 执行分组、排序和筛选并且结果显示在 <xref:System.Windows.Controls.DataGrid> UI 中。  
  
 ![DataGrid 中的分组数据](../../../../docs/framework/wpf/controls/media/wpf-datagridgroups.png "WPF\_DataGridGroups")  
在 DataGrid 中对数据分组  
  
## 使用 CollectionViewSource 作为 ItemsSource  
 若要在 <xref:System.Windows.Controls.DataGrid> 控件中对数据进行分组、排序和筛选，请将 <xref:System.Windows.Controls.DataGrid> 绑定到支持这些功能的 <xref:System.Windows.Data.CollectionView>。  在本示例中，<xref:System.Windows.Controls.DataGrid> 绑定到 <xref:System.Windows.Data.CollectionViewSource>，后者为 `Task` 对象的 <xref:System.Collections.Generic.List%601> 提供这些功能。  
  
#### 将 DataGrid 绑定到 CollectionViewSource  
  
1.  创建实现 <xref:System.Collections.IEnumerable> 接口的数据集合。  
  
     如果使用 <xref:System.Collections.Generic.List%601> 创建集合，则应创建一个继承自 <xref:System.Collections.Generic.List%601> 的新类，而不是实例化 <xref:System.Collections.Generic.List%601> 的实例。  这使您能够在 XAML 中将数据绑定到该集合。  
  
    > [!NOTE]
    >  该集合中的对象必须实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口和 <xref:System.ComponentModel.IEditableObject> 接口，以便 <xref:System.Windows.Controls.DataGrid> 对属性更改和编辑操作正确做出响应。  有关更多信息，请参见[实现属性更改通知](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md)。  
  
     [!code-csharp[DataGrid_GroupSortFilter#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#101)]
     [!code-vb[DataGrid_GroupSortFilter#101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#101)]  
  
2.  在 XAML 中，创建集合类的一个实例并设置 [x:Key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)。  
  
3.  在 XAML 中，创建 <xref:System.Windows.Data.CollectionViewSource> 类的一个实例，设置 [x:Key 指令](../../../../docs/framework/xaml-services/x-key-directive.md)，并将集合类的实例设置为 <xref:System.Windows.Data.CollectionViewSource.Source%2A>。  
  
     [!code-xml[DataGrid_GroupSortFilter#201](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/WindowSnips1.xaml#201)]  
  
4.  创建 <xref:System.Windows.Controls.DataGrid> 类的一个实例，并将 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性设置为 <xref:System.Windows.Data.CollectionViewSource>。  
  
     [!code-xml[DataGrid_GroupSortFilter#002](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#002)]  
  
5.  若要从代码访问 <xref:System.Windows.Data.CollectionViewSource>，请使用 <xref:System.Windows.Data.CollectionViewSource.GetDefaultView%2A> 方法获取对 <xref:System.Windows.Data.CollectionViewSource> 的引用。  
  
     [!code-csharp[DataGrid_GroupSortFilter#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#102)]
     [!code-vb[DataGrid_GroupSortFilter#102](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#102)]  
  
## 对 DataGrid 中的项分组  
 为了指定项在 <xref:System.Windows.Controls.DataGrid> 中的分组方式，使用 <xref:System.Windows.Data.PropertyGroupDescription> 类型对源视图中的项进行分组。  
  
#### 使用 XAML 在 DataGrid 中对项分组  
  
1.  创建一个 <xref:System.Windows.Data.PropertyGroupDescription>，它指定作为分组依据的属性。  可以在 XAML 或代码中指定该属性。  
  
    1.  在 XAML 中，将 <xref:System.Windows.Data.PropertyGroupDescription.PropertyName%2A> 设置为作为分组依据的属性的名称。  
  
    2.  在代码中，将作为分组依据的属性的名称传递给构造函数。  
  
2.  将 <xref:System.Windows.Data.PropertyGroupDescription> 添加到 <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A?displayProperty=fullName> 集合。  
  
3.  将 <xref:System.Windows.Data.PropertyGroupDescription> 的附加实例添加到 <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A> 集合，以便添加更多分组级别。  
  
     [!code-xml[DataGrid_GroupSortFilter#012](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#012)]  
  
     [!code-csharp[DataGrid_GroupSortFilter#112](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#112)]
     [!code-vb[DataGrid_GroupSortFilter#112](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#112)]  
  
4.  若要移除某个组，请从 <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A> 集合中移除 <xref:System.Windows.Data.PropertyGroupDescription>。  
  
5.  若要移除所有组，请调用 <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A> 集合的 <xref:System.Collections.ObjectModel.Collection%601.Clear%2A> 方法。  
  
     [!code-csharp[DataGrid_GroupSortFilter#114](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#114)]
     [!code-vb[DataGrid_GroupSortFilter#114](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#114)]  
  
 在 <xref:System.Windows.Controls.DataGrid> 中对项分组时，可以定义用于指定每个组的外观的 <xref:System.Windows.Controls.GroupStyle>。  可应用 <xref:System.Windows.Controls.GroupStyle>，方法是将其添加到 DataGrid 的 <xref:System.Windows.Controls.ItemsControl.GroupStyle%2A> 集合。  如果您具有多个分组级别，则可以将不同的样式应用于每个组级别。  应用样式的顺序与定义它们的顺序相同。  例如，如果您定义两个样式，则第一个样式将应用于顶级行组。  第二个样式将应用于第二个级别及其下的所有行组。  <xref:System.Windows.Controls.GroupStyle> 的 <xref:System.Windows.FrameworkElement.DataContext%2A> 是组表示的 <xref:System.Windows.Data.CollectionViewGroup>。  
  
#### 更改行组标头的外观  
  
1.  创建定义行组外观的 <xref:System.Windows.Controls.GroupStyle>。  
  
2.  将 <xref:System.Windows.Controls.GroupStyle> 放入 `<DataGrid.GroupStyle>` 标记中。  
  
     [!code-xml[DataGrid_GroupSortFilter#003](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#003)]  
  
## 对 DataGrid 中的项排序  
 若要指定项在 <xref:System.Windows.Controls.DataGrid> 中的排序方式，使用 <xref:System.ComponentModel.SortDescription> 类型对源视图中的项进行排序。  
  
#### 对 DataGrid 中的项进行排序  
  
1.  创建一个 <xref:System.ComponentModel.SortDescription>，它指定作为排序方式的属性。  可以在 XAML 或代码中指定该属性。  
  
    1.  在 XAML 中，将 <xref:System.ComponentModel.SortDescription.PropertyName%2A> 设置为作为排序方式的属性的名称。  
  
    2.  在代码中，将作为排序方式的属性的名称以及 <xref:System.ComponentModel.ListSortDirection> 传递给构造函数。  
  
2.  将 <xref:System.ComponentModel.SortDescription> 添加到 <xref:System.Windows.Data.CollectionViewSource.SortDescriptions%2A?displayProperty=fullName> 集合。  
  
3.  将 <xref:System.ComponentModel.SortDescription> 的附加实例添加到 <xref:System.Windows.Data.CollectionViewSource.SortDescriptions%2A> 集合，以便按附加的属性进行排序。  
  
     [!code-xml[DataGrid_GroupSortFilter#011](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#011)]  
  
     [!code-csharp[DataGrid_GroupSortFilter#211](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/WindowSnips1.xaml.cs#211)]
     [!code-vb[DataGrid_GroupSortFilter#211](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#211)]  
  
## 对 DataGrid 中的项进行筛选  
 若要使用 <xref:System.Windows.Data.CollectionViewSource> 在 <xref:System.Windows.Controls.DataGrid> 中对项进行筛选，请在 <xref:System.Windows.Data.CollectionViewSource.Filter?displayProperty=fullName> 事件的处理程序中提供筛选逻辑。  
  
#### 对 DataGrid 中的项进行筛选  
  
1.  为 <xref:System.Windows.Data.CollectionViewSource.Filter?displayProperty=fullName> 事件添加处理程序。  
  
2.  在 <xref:System.Windows.Data.CollectionViewSource.Filter> 事件处理程序中，定义筛选逻辑。  
  
     每次刷新视图时都会应用该筛选器。  
  
     [!code-xml[DataGrid_GroupSortFilter#013](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#013)]  
  
     [!code-csharp[DataGrid_GroupSortFilter#113](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#113)]
     [!code-vb[DataGrid_GroupSortFilter#113](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#113)]  
  
 或者，也可以通过创建提供筛选逻辑的方法，并将 <xref:System.Windows.Data.CollectionView.Filter%2A?displayProperty=fullName> 属性设置为应用该筛选器，在 <xref:System.Windows.Controls.DataGrid> 中对项进行筛选。  若要查看此方法的示例，请参见[筛选视图中的数据](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md)。  
  
## 示例  
 下面的示例演示如何在 <xref:System.Windows.Data.CollectionViewSource> 中对 `Task` 数据进行分组、排序和筛选，以及如何在 <xref:System.Windows.Controls.DataGrid> 中显示经过分组、排序和筛选的 `Task` 数据。  <xref:System.Windows.Data.CollectionViewSource> 用作 <xref:System.Windows.Controls.DataGrid> 的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>。  对 <xref:System.Windows.Data.CollectionViewSource> 执行分组、排序和筛选并且结果显示在 <xref:System.Windows.Controls.DataGrid> UI 中。  
  
 若要测试此示例，需要将 DGGroupSortFilterExample 名称调整为与项目名称匹配。  如果您使用的是 Visual Basic，则需要将 <xref:System.Windows.Window> 的类名更改为以下名称。  
  
 `<Window x:Class="MainWindow"`  
  
 [!code-xml[DataGrid_GroupSortFilter#000](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#000)]  
  
 [!code-csharp[DataGrid_GroupSortFilter#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#100)]
 [!code-vb[DataGrid_GroupSortFilter#100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#100)]  
  
## 编译代码  
  
## 可靠编程  
  
## .NET Framework 安全性  
  
## 请参阅  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [创建和绑定到 ObservableCollection](../../../../docs/framework/wpf/data/how-to-create-and-bind-to-an-observablecollection.md)   
 [筛选视图中的数据](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md)   
 [在视图中对数据进行排序](../../../../docs/framework/wpf/data/how-to-sort-data-in-a-view.md)   
 [在 XAML 中使用视图对数据进行排序和分组](../../../../docs/framework/wpf/data/how-to-sort-and-group-data-using-a-view-in-xaml.md)