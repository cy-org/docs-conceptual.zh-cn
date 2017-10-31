---
title: "DataGrid | Microsoft Docs"
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
  - "控件 [WPF], DataGrid"
  - "DataGrid [WPF], 常规任务"
  - "DataGrid [WPF], 自定义外观"
  - "DataGrid 列类型 [WPF]"
  - "DataGrid 列 [WPF], using"
  - "DataGrid 控件 [WPF]"
  - "DataGrid 方案 [WPF]"
ms.assetid: bf89ea63-79b6-422b-bc9f-0485ad803216
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# DataGrid
使用 <xref:System.Windows.Controls.DataGrid> 控件可以显示和编辑来自多个不同源（例如，来自 SQL 数据库、LING 查询或任何其他可绑定的数据源）的数据。  有关更多信息，请参见[绑定源概述](../../../../docs/framework/wpf/data/binding-sources-overview.md)。  
  
 列可以显示文本、控件（例如 <xref:System.Windows.Controls.ComboBox>）或任何其他 WPF 内容（例如图像、按钮）或包含在模板中的任何内容。  您可以使用 <xref:System.Windows.Controls.DataGridTemplateColumn> 显示模板中已定义的数据。  下表列出了默认情况下提供的列类型。  
  
|生成的列类型|数据类型|  
|------------|----------|  
|<xref:System.Windows.Controls.DataGridTextColumn>|<xref:System.String>|  
|<xref:System.Windows.Controls.DataGridCheckBoxColumn>|<xref:System.Boolean>|  
|<xref:System.Windows.Controls.DataGridComboBoxColumn>|<xref:System.Enum>|  
|<xref:System.Windows.Controls.DataGridHyperlinkColumn>|<xref:System.Uri>|  
  
 <xref:System.Windows.Controls.DataGrid> 可对外观（例如单元格字体、颜色和大小）进行自定义。  <xref:System.Windows.Controls.DataGrid> 支持其他 WPF 控件的所有样式和模板化功能。  <xref:System.Windows.Controls.DataGrid> 还包括用于编辑、排序及验证的默认和可自定义的行为。  
  
 下表列出了针对 <xref:System.Windows.Controls.DataGrid> 的一些常规任务以及完成这些任务的方法。  通过查看相关 API，您可以找到更多信息和代码示例。  
  
|方案|方法|  
|--------|--------|  
|交替的背景色|将 <xref:System.Windows.Controls.ItemsControl.AlternationIndex%2A> 属性设置为 2 或更多，然后向 <xref:System.Windows.Controls.DataGrid.RowBackground%2A> 和 <xref:System.Windows.Controls.DataGrid.AlternatingRowBackground%2A> 属性分配 <xref:System.Windows.Media.Brush>。|  
|定义单元格和行选择行为|设置 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 和 <xref:System.Windows.Controls.DataGrid.SelectionUnit%2A> 属性。|  
|自定义标题、单元格和行的可视外观|将新的 <xref:System.Windows.Style> 应用于 <xref:System.Windows.Controls.DataGrid.ColumnHeaderStyle%2A>、<xref:System.Windows.Controls.DataGrid.RowHeaderStyle%2A>、<xref:System.Windows.Controls.DataGrid.CellStyle%2A> 或 <xref:System.Windows.Controls.DataGrid.RowStyle%2A> 属性。|  
|设置调整大小选项|设置 <xref:System.Windows.FrameworkElement.Height%2A>、<xref:System.Windows.FrameworkElement.MaxHeight%2A>、<xref:System.Windows.FrameworkElement.MinHeight%2A>、<xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.MaxWidth%2A> 或 <xref:System.Windows.FrameworkElement.MinWidth%2A> 属性。  有关更多信息，请参见 [DataGrid 控件中的调整大小选项](../../../../docs/framework/wpf/controls/sizing-options-in-the-datagrid-control.md)。|  
|访问选定项|检查 <xref:System.Windows.Controls.DataGrid.SelectedCells%2A> 属性以获取选定单元格并检查 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems%2A> 属性以获取选定行。  有关更多信息，请参见 <xref:System.Windows.Controls.DataGrid.SelectedCells%2A>。|  
|自定义最终用户交互|设置 <xref:System.Windows.Controls.DataGrid.CanUserAddRows%2A>、<xref:System.Windows.Controls.DataGrid.CanUserDeleteRows%2A>、<xref:System.Windows.Controls.DataGrid.CanUserReorderColumns%2A>、<xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A>、<xref:System.Windows.Controls.DataGrid.CanUserResizeRows%2A> 和 <xref:System.Windows.Controls.DataGrid.CanUserSortColumns%2A> 属性。|  
|取消或更改自动生成的列|处理 <xref:System.Windows.Controls.DataGrid.AutoGeneratingColumn> 事件。|  
|冻结列|将 <xref:System.Windows.Controls.DataGrid.FrozenColumnCount%2A> 属性设置为 1，并通过将 <xref:System.Windows.Controls.DataGridColumn.DisplayIndex%2A> 属性设置为 0 将列移动到最左边的位置。|  
|使用 XML 数据作为数据源|将 <xref:System.Windows.Controls.DataGrid> 上的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 绑定到表示项集合的 XPath 查询。  在 <xref:System.Windows.Controls.DataGrid> 中创建每个列。  通过将绑定上的 XPath 设置为获取项源上属性的查询来绑定每个列。  有关示例，请参见<xref:System.Windows.Controls.DataGridTextColumn>。|  
  
## 相关主题  
  
|标题|说明|  
|--------|--------|  
|[演练：在 DataGrid 控件中显示 SQL Server 数据库中的数据](../../../../docs/framework/wpf/controls/walkthrough-display-data-from-a-sql-server-database-in-a-datagrid-control.md)|描述如何设置新的 WPF 项目、添加实体框架元素、设置源并在 <xref:System.Windows.Controls.DataGrid> 中显示数据。|  
|[如何：向 DataGrid 控件中添加行详细信息](../../../../docs/framework/wpf/controls/how-to-add-row-details-to-a-datagrid-control.md)|描述如何为 <xref:System.Windows.Controls.DataGrid> 创建行详细信息。|  
|[如何：用 DataGrid 控件实现验证](../../../../docs/framework/wpf/controls/how-to-implement-validation-with-the-datagrid-control.md)|描述如何验证 <xref:System.Windows.Controls.DataGrid> 单元格和行中的值，并显示验证反馈。|  
|[DataGrid 控件中的默认键盘和鼠标行为](../../../../docs/framework/wpf/controls/default-keyboard-and-mouse-behavior-in-the-datagrid-control.md)|描述如何使用键盘和鼠标与 <xref:System.Windows.Controls.DataGrid> 控件进行交互。|  
|[如何：在 DataGrid 控件中对数据进行分组、排序和筛选](../../../../docs/framework/wpf/controls/how-to-group-sort-and-filter-data-in-the-datagrid-control.md)|描述如何通过对数据进行分组、排序和筛选，以不同方式在 <xref:System.Windows.Controls.DataGrid> 中查看数据。|  
|[DataGrid 控件中的调整大小选项](../../../../docs/framework/wpf/controls/sizing-options-in-the-datagrid-control.md)|描述如何在 <xref:System.Windows.Controls.DataGrid> 中控制绝对大小调整和自动大小调整。|  
  
## 请参阅  
 <xref:System.Windows.Controls.DataGrid>   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [控件](../../../../docs/framework/wpf/controls/index.md)   
 [WPF 内容模型](../../../../docs/framework/wpf/controls/wpf-content-model.md)