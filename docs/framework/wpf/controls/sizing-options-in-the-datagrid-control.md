---
title: "DataGrid 控件中的调整大小选项 | Microsoft Docs"
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
  - "自动调整 DataGrid 的大小"
  - "DataGrid 控件 [WPF], 调整大小"
  - "大小 [WPF], DataGrid"
ms.assetid: 96a0e47e-b010-4302-98ef-2daac446d8db
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# DataGrid 控件中的调整大小选项
有很多选项可用于控制 <xref:System.Windows.Controls.DataGrid> 自身调整大小的方式。  可以将 <xref:System.Windows.Controls.DataGrid> 以及 <xref:System.Windows.Controls.DataGrid> 中的各个列和行设置为自动调整大小以容纳内容，或者可以设置为特定值。  默认情况下，<xref:System.Windows.Controls.DataGrid> 将根据内容的大小相应地放大和缩小。  
  
## 调整 DataGrid 的大小  
  
### 使用自动调整大小时要小心  
 默认情况下，将 <xref:System.Windows.Controls.DataGrid> 的 <xref:System.Windows.FrameworkElement.Height%2A> 和 <xref:System.Windows.FrameworkElement.Width%2A> 属性设置为 <xref:System.Double.NaN?displayProperty=fullName>（XAML 中为“`Auto`”），<xref:System.Windows.Controls.DataGrid> 将根据内容大小进行调整。  
  
 放置在不限制其子级大小的容器（如 <xref:System.Windows.Controls.Canvas> 或 <xref:System.Windows.Controls.StackPanel>）中时，<xref:System.Windows.Controls.DataGrid> 将拉伸到超过容器的可见边界，而滚动条将不显示。  此情况要综合考虑可用性和性能因素。  
  
 绑定到数据集时，如果未限制 <xref:System.Windows.Controls.DataGrid> 的 <xref:System.Windows.FrameworkElement.Height%2A>，它将继续为所绑定数据集中的每个数据项添加一行。  随着行的增加，这可能导致 <xref:System.Windows.Controls.DataGrid> 放大到超过您应用程序的可见边界。  在这种情况下，<xref:System.Windows.Controls.DataGrid> 将不显示滚动条，因为其 <xref:System.Windows.FrameworkElement.Height%2A> 将继续增大以容纳新行。  
  
 为 <xref:System.Windows.Controls.DataGrid> 中的每行创建一个对象。  如果您正在使用大型数据集并允许 <xref:System.Windows.Controls.DataGrid> 自己自动调整大小，则大量对象的创建可能影响您应用程序的性能。  
  
 为了在使用大型数据集时避免这些问题，建议您特别设置 <xref:System.Windows.Controls.DataGrid> 的 <xref:System.Windows.FrameworkElement.Height%2A> 或将其放置在限制 <xref:System.Windows.FrameworkElement.Height%2A> 的容器（如 <xref:System.Windows.Controls.Grid>）中。  限制 <xref:System.Windows.FrameworkElement.Height%2A> 时，<xref:System.Windows.Controls.DataGrid> 将只创建在指定的 <xref:System.Windows.FrameworkElement.Height%2A> 中容纳的行数，并根据显示新数据的需要回收这些行。  
  
### 设置 DataGrid 大小  
 可以将 <xref:System.Windows.Controls.DataGrid> 设置为在指定边界内自动调整大小，或将 <xref:System.Windows.Controls.DataGrid> 设置为特定大小。  下表显示可以设置用来控制 <xref:System.Windows.Controls.DataGrid> 大小的属性。  
  
|属性|说明|  
|--------|--------|  
|<xref:System.Windows.FrameworkElement.Height%2A>|为 <xref:System.Windows.Controls.DataGrid> 设置特定高度。|  
|<xref:System.Windows.FrameworkElement.MaxHeight%2A>|设置 <xref:System.Windows.Controls.DataGrid> 的高度上限。  <xref:System.Windows.Controls.DataGrid> 将垂直增大，直到其达到此高度。|  
|<xref:System.Windows.FrameworkElement.MinHeight%2A>|设置 <xref:System.Windows.Controls.DataGrid> 的高度下限。  <xref:System.Windows.Controls.DataGrid> 将垂直收缩，直到其达到此高度。|  
|<xref:System.Windows.FrameworkElement.Width%2A>|为 <xref:System.Windows.Controls.DataGrid> 设置特定宽度。|  
|<xref:System.Windows.FrameworkElement.MaxWidth%2A>|设置 <xref:System.Windows.Controls.DataGrid> 的宽度上限。  <xref:System.Windows.Controls.DataGrid> 将水平增大，直到其达到此宽度。|  
|<xref:System.Windows.FrameworkElement.MinWidth%2A>|设置 <xref:System.Windows.Controls.DataGrid> 的宽度下限。  <xref:System.Windows.Controls.DataGrid> 将水平收缩，直到其达到此宽度。|  
  
## 调整行和行标题的大小  
  
### DataGrid 行  
 默认情况下，将 <xref:System.Windows.Controls.DataGrid> 行的 <xref:System.Windows.FrameworkElement.Height%2A> 属性设置为 <xref:System.Double.NaN?displayProperty=fullName>（XAML 中为“`Auto`”），行高度将增大以适合内容大小。  可以通过设置 <xref:System.Windows.Controls.DataGrid.RowHeight%2A?displayProperty=fullName> 属性指定 <xref:System.Windows.Controls.DataGrid> 中所有行的高度。  用户可以通过拖动行标题分隔符来更改行高度。  
  
### DataGrid 行标题  
 若要显示行标题，<xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A> 属性必须设置为 <xref:System.Windows.Controls.DataGridHeadersVisibility?displayProperty=fullName> 或 <xref:System.Windows.Controls.DataGridHeadersVisibility?displayProperty=fullName>。  默认情况下会显示行标题，并且行标题将自动调整大小以适合其内容。  可以通过设置 <xref:System.Windows.Controls.DataGrid.RowHeaderWidth%2A?displayProperty=fullName> 属性为行标题指定特定宽度。  
  
## 调整列和列标题的大小  
  
### DataGrid 列  
 <xref:System.Windows.Controls.DataGrid> 使用 <xref:System.Windows.Controls.DataGridLength> 和 <xref:System.Windows.Controls.DataGridLengthUnitType> 结构的值来指定绝对或自动调整大小模式。  
  
 下表显示 <xref:System.Windows.Controls.DataGridLengthUnitType> 结构提供的值。  
  
|名称|说明|  
|--------|--------|  
|<xref:System.Windows.Controls.DataGridLengthUnitType>|默认自动调整大小模式同时根据单元格和列标题的内容调整 <xref:System.Windows.Controls.DataGrid> 列的大小。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType>|基于单元格的自动调整大小模式根据列中单元格的内容（不包括列标题）调整 <xref:System.Windows.Controls.DataGrid> 列的大小。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType>|基于标题的自动调整大小模式仅根据列标题的内容调整 <xref:System.Windows.Controls.DataGrid> 列的大小。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType>|基于像素的调整大小模式根据提供的数值调整 <xref:System.Windows.Controls.DataGrid> 列的大小。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType>|星号调整大小模式用于根据加权比例分配可用空间。<br /><br /> 在 XAML 中，星号值用 n\* 表示，其中 n 表示数值。  1\* 等效于 \*。  例如，如果 <xref:System.Windows.Controls.DataGrid> 中两列的宽度为 \* 和 2\*，则第一列应接收可用空间的一个份额，第二列应接收可用空间的两个份额。|  
  
 <xref:System.Windows.Controls.DataGridLengthConverter> 类可用于在数值或字符串值与 <xref:System.Windows.Controls.DataGridLength> 值之间进行数据转换。  
  
 默认情况下，<xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=fullName> 属性设置为 <xref:System.Windows.Controls.DataGridLength.SizeToHeader%2A>，<xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=fullName> 属性设置为 <xref:System.Windows.Controls.DataGridLength.Auto%2A>。  将调整大小模式设置为 <xref:System.Windows.Controls.DataGridLength.Auto%2A> 或 <xref:System.Windows.Controls.DataGridLength.SizeToCells%2A> 时，列将增大到达到最宽可见内容的宽度。  滚动时，如果大于当前列大小的内容滚动到视图中，则这些调整大小模式将导致列增大。  当内容滚出视图之外时，此列将不缩小。  
  
 可以将 <xref:System.Windows.Controls.DataGrid> 中的列设置为仅在指定边界内自动调整大小，或将列设置为特定大小。  下表显示可以设置用来控制列大小的属性。  
  
|属性|说明|  
|--------|--------|  
|<xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=fullName>|为 <xref:System.Windows.Controls.DataGrid> 中的所有列设置上限。|  
|<xref:System.Windows.Controls.DataGridColumn.MaxWidth%2A?displayProperty=fullName>|为单个列设置上限。  重写 <xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=fullName>。|  
|<xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=fullName>|为 <xref:System.Windows.Controls.DataGrid> 中的所有列设置下限。|  
|<xref:System.Windows.Controls.DataGridColumn.MinWidth%2A?displayProperty=fullName>|为单个列设置下限。  重写 <xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=fullName>。|  
|<xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=fullName>|为 <xref:System.Windows.Controls.DataGrid> 中的所有列设置特定宽度。|  
|<xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=fullName>|为单个列设置特定宽度。  重写 <xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=fullName>。|  
  
### DataGrid 列标题  
 默认情况下，显示 <xref:System.Windows.Controls.DataGrid> 列标题。  若要隐藏列标题，必须将 <xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A> 属性设置为 <xref:System.Windows.Controls.DataGridHeadersVisibility?displayProperty=fullName> 或 <xref:System.Windows.Controls.DataGridHeadersVisibility?displayProperty=fullName>。  默认情况下，当显示列标题时，列标题将自动调整大小以适合其内容。  可以通过设置 <xref:System.Windows.Controls.DataGrid.ColumnHeaderHeight%2A?displayProperty=fullName> 属性为列标题指定特定高度。  
  
### 用鼠标调整大小  
 用户可以通过拖动行或列标题分隔符来调整 <xref:System.Windows.Controls.DataGrid> 行和列的大小。  <xref:System.Windows.Controls.DataGrid> 还支持通过双击行标题或列标题分隔符来自动调整行和列的大小。  若要防止用户调整特定列的大小，请将这些列的 <xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=fullName> 属性设置为 `false`。  若要防止用户调整所有列的大小，请将 <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=fullName> 属性设置为 `false`。  若要防止用户调整所有行的大小，请将 <xref:System.Windows.Controls.DataGrid.CanUserResizeRows%2A?displayProperty=fullName> 属性设置为 `false`。  
  
## 请参阅  
 <xref:System.Windows.Controls.DataGrid>   
 <xref:System.Windows.Controls.DataGridColumn>   
 <xref:System.Windows.Controls.DataGridLength>   
 <xref:System.Windows.Controls.DataGridLengthConverter>