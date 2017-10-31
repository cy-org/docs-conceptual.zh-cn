---
title: "如何：向 DataGrid 控件中添加行详细信息 | Microsoft Docs"
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
  - "DataGrid [WPF], 行详细信息"
  - "DataTemplate [WPF], DataGrid"
  - "行详细信息 [WPF], DataGrid"
ms.assetid: 0bdc6f50-9b4c-483f-9df6-a47a1fde998b
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：向 DataGrid 控件中添加行详细信息
在使用 <xref:System.Windows.Controls.DataGrid> 控件时，可以通过添加行详细信息部分来自定义数据显示。  通过添加行详细信息部分，可以对可显示或折叠的模板中的一些数据进行分组。  例如，可以向只为 <xref:System.Windows.Controls.DataGrid> 中的每行显示数据摘要，但在用户选择行时显示更多数据字段的 <xref:System.Windows.Controls.DataGrid> 添加行详细信息。  用 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 属性为行详细信息部分定义模板。  下图显示一个行详细信息部分的示例。  
  
 ![与行详细信息一起显示的 DataGrid](../../../../docs/framework/wpf/controls/media/ndp-rowdetails.png "NDP\_RowDetails")  
  
 可以将行详细信息模板定义为内联 XAML 或资源。  下面的过程演示了这两种方法。  在整个项目周期中可使用作为资源添加的数据模板，而不用重新创建模板。  作为内联 XAML 添加的数据模板只能从定义它的控件进行访问。  
  
### 使用内联 XAML 显示行详细信息  
  
1.  创建显示来自数据源的数据的 <xref:System.Windows.Controls.DataGrid>。  
  
2.  在 <xref:System.Windows.Controls.DataGrid> 元素中添加一个 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 元素。  
  
3.  创建定义行详细信息部分外观的 <xref:System.Windows.DataTemplate>。  
  
     下面的 XAML 演示 <xref:System.Windows.Controls.DataGrid> 以及如何以内联方式定义 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A>。  <xref:System.Windows.Controls.DataGrid> 在每行中显示三个值，在选择行时显示另外三个值。  
  
     [!code-xml[DataGrid_RowDetails#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml#1)]  
  
     下面的代码演示如何使用查询选择显示在 <xref:System.Windows.Controls.DataGrid> 中的数据。  在此示例中，查询从包含客户信息的实体中选择数据。  
  
     [!code-csharp[DataGrid_RowDetails#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml.cs#2)]
     [!code-vb[DataGrid_RowDetails#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_rowdetails/vb/mainwindow.xaml.vb#2)]  
  
### 使用资源显示行详细信息  
  
1.  创建显示来自数据源的数据的 <xref:System.Windows.Controls.DataGrid>。  
  
2.  将 <xref:System.Windows.FrameworkElement.Resources%2A> 元素添加到根元素（例如 <xref:System.Windows.Window> 控件或 <xref:System.Windows.Controls.Page> 控件），或将 <xref:System.Windows.Application.Resources%2A> 元素添加到 App.xaml（又名 Application.xaml）文件中的 <xref:System.Windows.Application> 类。  
  
3.  在资源元素中，创建定义行详细信息部分外观的 <xref:System.Windows.DataTemplate>。  
  
     下面的 XAML 演示 <xref:System.Windows.Application> 类中定义的 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A>。  
  
     [!code-xml[DataGrid_RowDetails#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/app.xaml#3)]  
  
4.  在 <xref:System.Windows.DataTemplate> 上，将 [x:Key 指令](../../../../docs/framework/xaml-services/x-key-directive.md) 设置为唯一标识数据模板的值。  
  
5.  在 <xref:System.Windows.Controls.DataGrid> 元素中，将 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 属性设置为在上述步骤中定义的资源。  将资源指定为静态资源。  
  
     下面的 XAML 演示上例中设置为资源的 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 属性。  
  
     [!code-xml[DataGrid_RowDetails#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/window2.xaml#4)]  
  
### 设置可见性并禁止行详细信息水平滚动  
  
1.  如果需要，将 <xref:System.Windows.Controls.DataGrid.RowDetailsVisibilityMode%2A> 属性设置为 <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode> 值。  
  
     默认情况下，该值设置为 <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode>。  将该值设置为 <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode> 可以显示所有行的详细信息，将该值设置为 <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode> 可以隐藏所有行的详细信息。  
  
2.  如果需要，可将 <xref:System.Windows.Controls.DataGrid.AreRowDetailsFrozen%2A> 属性设置为 `true` 以禁止行详细信息部分水平滚动。