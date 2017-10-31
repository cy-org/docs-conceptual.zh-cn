---
title: "Windows 窗体 DataGridView 控件中的列排序模式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "数据网格, 排序模式"
  - "DataGridView 控件 [Windows 窗体], 排序模式"
ms.assetid: 43715887-2df9-4da7-bcf1-b9c7c842b2bf
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Windows 窗体 DataGridView 控件中的列排序模式
<xref:System.Windows.Forms.DataGridView> 列有三种排序模式。  每一列的排序模式是通过该列的 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 属性指定的，该属性可以设置为以下的 <xref:System.Windows.Forms.DataGridViewColumnSortMode> 枚举值之一。  
  
|`DataGridViewColumnSortMode` 值|说明|  
|------------------------------------|--------|  
|<xref:System.Windows.Forms.DataGridViewColumnSortMode>|文本框列的默认排序模式。  除非将列标头用于选择，否则单击列标头将自动按此列对 <xref:System.Windows.Forms.DataGridView> 排序，并显示一个指示排序顺序的标志符号。|  
|<xref:System.Windows.Forms.DataGridViewColumnSortMode>|非文本框列的默认排序模式。  可以以编程方式对此列排序；但此列不适合排序，因此未为排序标志符号保留空间。|  
|<xref:System.Windows.Forms.DataGridViewColumnSortMode>|可以以编程方式对此列排序；而且为排序标志符号保留了空间。|  
  
 如果默认为 <xref:System.Windows.Forms.DataGridViewColumnSortMode> 的列包含的值可以有意义地排序，您可能希望更改该列的排序模式。  例如，如果有一个数据库列包含表示项状态的数字，则可以通过将一个图像列绑定到该数据库列来将这些数字显示为相应的图标。  然后可以在 <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=fullName> 事件的处理程序中，将数值单元格值更改为图像显示值。  在这种情况下，将 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewColumnSortMode> 会使用户能够对该列排序。  自动排序将使用户能够对具有相同状态的项分组，即使这些对应于数字的状态没有自然的顺序。  复选框列也是自动排序对于将处于相同状态的项分组很有用的示例。  
  
 可以以编程方式按任一列或多列中的值对 <xref:System.Windows.Forms.DataGridView> 排序，而不论 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 设置如何。  当希望为排序提供自己的用户界面 \(UI\) 时，或者当希望实现自定义排序时，以编程方式排序很有用。  提供自己的排序用户界面非常有用，例如，在设置 <xref:System.Windows.Forms.DataGridView> 选择模式以启用列标头选择时。  在这种情况下，虽然列标头不能用于排序，但是仍希望标头显示相应的排序标志符号，因此将 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewColumnSortMode>。  
  
 设置为编程排序模式的列不会自动显示排序标志符号。  对于这些列，必须通过设置 <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.SortGlyphDirection%2A?displayProperty=fullName> 属性来手动显示标志符号。  为了在自定义排序中能够灵活操作，这是必需的。  例如，如果按多列对 <xref:System.Windows.Forms.DataGridView> 排序，则可能希望显示多个排序标志符号或不显示任何标志符号。  
  
 虽然可以以编程方式按任一列对 <xref:System.Windows.Forms.DataGridView> 排序，但是一些列（如按钮列）可能不包含可以有意义地排序的值。  对于这些列，<xref:System.Windows.Forms.DataGridViewColumnSortMode> 的 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 属性设置指示将永不使用这些列排序，因此不需要在标头中为标志符号保留空间。  
  
 对于已排序的 <xref:System.Windows.Forms.DataGridView>，可以通过检查 <xref:System.Windows.Forms.DataGridView.SortedColumn%2A> 和 <xref:System.Windows.Forms.DataGridView.SortOrder%2A> 属性的值确定排序列和排序顺序。  这些值在自定义排序操作之后没有意义。  有关自定义排序的更多信息，请参见本主题后面的“自定义排序”部分。  
  
 对包含绑定列和未绑定列的 <xref:System.Windows.Forms.DataGridView> 控件排序时，未绑定列中的值无法自动维护。  若要维护这些值，必须通过将 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性设置为 `true` 和处理 <xref:System.Windows.Forms.DataGridView.CellValueNeeded> 和 <xref:System.Windows.Forms.DataGridView.CellValuePushed> 事件实现虚拟模式。  有关更多信息，请参见 [如何：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/how-to-implement-virtual-mode-in-the-windows-forms-datagridview-control.md)。  在绑定模式下按未绑定列进行排序不受支持。  
  
## 以编程方式进行排序  
 可以通过调用 <xref:System.Windows.Forms.DataGridView> 的 <xref:System.Windows.Forms.DataGridView.Sort%2A> 方法以编程方式对其排序。  
  
 <xref:System.Windows.Forms.DataGridView.Sort%2A> 方法的 `Sort(DataGridViewColumn,ListSortDirection)` 重载采用 <xref:System.Windows.Forms.DataGridViewColumn> 和 <xref:System.ComponentModel.ListSortDirection> 枚举值作为参数。  当按列值可以有意义地排序（但不想将该列配置为用于自动排序）的列排序时，此重载很有用。  当调用此重载并传入具有 <xref:System.Windows.Forms.DataGridViewColumnSortMode?displayProperty=fullName> 的 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 属性值的列时，会自动设置 <xref:System.Windows.Forms.DataGridView.SortedColumn%2A> 和 <xref:System.Windows.Forms.DataGridView.SortOrder%2A> 属性并在列标头中显示相应的排序标志符号。  
  
> [!NOTE]
>  当通过设置 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 属性将 <xref:System.Windows.Forms.DataGridView> 控件绑定到外部数据源时，`Sort(DataGridViewColumn,ListSortDirection)` 方法重载不能用于未绑定列。  此外，当 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性为 `true` 时，可以仅为绑定列调用此重载。  若要确定某一列是否为数据绑定列，请检查 <xref:System.Windows.Forms.DataGridViewColumn.IsDataBound%2A> 属性值。  在绑定模式下对未绑定列排序不受支持。  
  
## 自定义排序  
 可以通过使用 <xref:System.Windows.Forms.DataGridView.Sort%2A> 方法的 `Sort(IComparer)` 重载或通过处理 <xref:System.Windows.Forms.DataGridView.SortCompare> 事件来自定义 <xref:System.Windows.Forms.DataGridView>。  
  
 `Sort(IComparer)` 方法重载采用一个实现 <xref:System.Collections.IComparer> 接口的类的一个实例作为参数。  当希望提供自定义排序时，此重载很有用；例如，当某一列中的值没有自然排序顺序时，或者当自然排序顺序不适用时。  在这种情况下，不能使用自动排序，但是可能仍然希望用户通过单击列标头进行排序。  可以在 <xref:System.Windows.Forms.DataGridView.ColumnHeaderMouseClick> 事件的处理程序中调用此重载，即使不使用列标头进行选择。  
  
> [!NOTE]
>  仅当 <xref:System.Windows.Forms.DataGridView> 控件未绑定到外部数据源且 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性值为 `false` 时，`Sort(IComparer)` 方法重载才起作用。  若要为绑定到外部数据源的列自定义排序，必须使用由该数据源提供的排序操作。  在虚拟模式中，必须为未绑定列提供您自己的排序操作。  
  
 若要使用 `Sort(IComparer)` 方法重载，必须创建您自己的类，该类实现 <xref:System.Collections.IComparer> 接口。  此接口要求您的类实现 <xref:System.Collections.IComparer.Compare%2A?displayProperty=fullName> 方法，在调用 `Sort(IComparer)` 方法重载时，<xref:System.Windows.Forms.DataGridView> 将 <xref:System.Windows.Forms.DataGridViewRow> 对象作为输入传给该方法。  使用此方法，您可以基于任一列中的值计算正确的行排序。  
  
 `Sort(IComparer)` 方法重载不设置 <xref:System.Windows.Forms.DataGridView.SortedColumn%2A> 和 <xref:System.Windows.Forms.DataGridView.SortOrder%2A> 属性，因此必须总是设置 <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.SortGlyphDirection%2A?displayProperty=fullName> 属性以显示排序标志符号。  
  
 作为 `Sort(IComparer)` 方法重载的一个替代方法，可以通过为 <xref:System.Windows.Forms.DataGridView.SortCompare> 事件实现处理程序来提供自定义排序。  当用户单击为自动排序配置的列的标头时，或者当调用 <xref:System.Windows.Forms.DataGridView.Sort%2A> 方法的 `Sort(DataGridViewColumn,ListSortDirection)` 重载时，将发生此事件。  对控件中的每对行均发生该事件，这使您能够计算它们的正确顺序。  
  
> [!NOTE]
>  当 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 属性已设置时，或者当 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性值为 `true` 时，不会发生 <xref:System.Windows.Forms.DataGridView.SortCompare> 事件。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.Sort%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.SortedColumn%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.SortOrder%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.SortGlyphDirection%2A?displayProperty=fullName>   
 [对 Windows 窗体 DataGridView 控件中的数据排序](../../../../docs/framework/winforms/controls/sorting-data-in-the-windows-forms-datagridview-control.md)   
 [如何：设置 Windows 窗体 DataGridView 控件中列的排序模式](../../../../docs/framework/winforms/controls/set-the-sort-modes-for-columns-wf-datagridview-control.md)   
 [如何：自定义 Windows 窗体 DataGridView 控件中的排序方式](../../../../docs/framework/winforms/controls/how-to-customize-sorting-in-the-windows-forms-datagridview-control.md)