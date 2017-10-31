---
title: "缩放 Windows 窗体 DataGridView 控件的最佳做法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "最佳做法, DataGridView 控件"
  - "数据网格, 最佳做法"
  - "DataGridView 控件 [Windows 窗体], 最佳做法"
  - "DataGridView 控件 [Windows 窗体], 行共享"
  - "DataGridView 控件 [Windows 窗体], 缩放"
  - "DataGridView 控件 [Windows 窗体], 共享行"
ms.assetid: 8321a8a6-6340-4fd1-b475-fa090b905aaf
caps.latest.revision: 31
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 31
---
# 缩放 Windows 窗体 DataGridView 控件的最佳做法
<xref:System.Windows.Forms.DataGridView> 控件的设计目的是提供最大的伸缩性。  如果需要显示大量数据，请遵循本主题中所描述的准则，以避免耗费大量内存或降低用户界面（UI）的响应能力。  本主题讨论下列问题：  
  
-   有效使用单元格样式  
  
-   有效使用快捷菜单  
  
-   有效使用自动大小调整  
  
-   有效使用选定单元格、行和列的集合  
  
-   使用共享行  
  
-   防止行成为非共享行  
  
 如果有特殊的性能需求，您可以实现虚拟模式并提供自己的数据管理操作。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件中的数据显示模式](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md)。  
  
## 有效使用单元格样式  
 每一个单元格、行和列都有其自己的样式信息。  样式信息存储在 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象中。  为许多单个 <xref:System.Windows.Forms.DataGridView> 元素创建单元格样式对象是低效的，特别是处理大量数据时。  为避免对性能的影响，请遵循以下准则：  
  
-   避免为单个 <xref:System.Windows.Forms.DataGridViewCell> 或 <xref:System.Windows.Forms.DataGridViewRow> 对象设置单元格样式属性。  这包括由 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A> 属性指定的行对象。  每一个从行模板克隆出来的新行将接收模板单元格样式对象的自身复制。  为了具有最大的伸缩性，请在 <xref:System.Windows.Forms.DataGridView> 级别设置单元格样式属性。  例如，设置 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName> 属性而不是设置 <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName> 属性。  
  
-   如果某些单元格需要默认格式以外的其他格式，可在单元格、行或列组中使用同一个 <xref:System.Windows.Forms.DataGridViewCellStyle> 实例。  避免在单个单元格、行和列上直接设置 <xref:System.Windows.Forms.DataGridViewCellStyle> 类型的属性。  有关单元格样式共享的示例，请参见 [如何：设置 Windows 窗体 DataGridView 控件的默认单元格样式](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)。  当通过处理 <xref:System.Windows.Forms.DataGridView.CellFormatting> 事件处理程序来分别设置单元格样式时，也可以避免对性能的影响。  有关示例，请参见[如何：自定义 Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)。  
  
-   当确定一个单元格样式时，请使用 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A?displayProperty=fullName> 属性而不要使用 <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName> 属性。  如果该属性尚未使用，访问 <xref:System.Windows.Forms.DataGridViewCell.Style%2A> 属性可以创建 <xref:System.Windows.Forms.DataGridViewCellStyle> 类的新实例。  另外，如果某些样式是从行、列或者控件继承的，该对象可能不包含完整的单元格样式信息。  有关单元格样式继承的更多信息，请参见 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)。  
  
## 有效使用快捷菜单  
 每一个单元格、行和列都有其自己的快捷菜单。  <xref:System.Windows.Forms.DataGridView> 控件中的快捷菜单由 <xref:System.Windows.Forms.ContextMenuStrip> 控件表示。  正如单元格样式对象一样，逐个地为众多 <xref:System.Windows.Forms.DataGridView> 元素创建快捷菜单将会给性能带来负面影响。  为了避免这种性能影响，请遵循以下准则：  
  
-   避免为单个单元格和行创建快捷菜单。  这包括行模板，向控件添加新行时行模板与其快捷菜单一起被复制。  为了获得最大的伸缩性，仅使用控件的 <xref:System.Windows.Forms.Control.ContextMenuStrip%2A> 属性为整个控件指定同一个快捷菜单。  
  
-   如果有多个行或单元格需要多个快捷菜单，可处理 <xref:System.Windows.Forms.DataGridView.CellContextMenuStripNeeded> 或 <xref:System.Windows.Forms.DataGridView.RowContextMenuStripNeeded> 事件。  这些事件使您可以自己管理快捷菜单对象，从而允许您对性能进行调整。  
  
## 有效使用自动大小调整  
 如果单元格内容发生更改，行、列和标题可以自动调整大小，以使单元格的整个内容能够完整地显示。  更改调整大小模式也可以调整行、列和标题的大小。  为了确定正确的大小，<xref:System.Windows.Forms.DataGridView> 控件必须检查每一个单元格所容纳的值。  当处理大数据集时，如果发生自动大小调整，这种分析可使控件的性能下降。  为了避免性能下降，请遵循以下准则：  
  
-   在具有大型行集的 <xref:System.Windows.Forms.DataGridView> 控件上，避免使用自动大小调整。  如果一定要使用自动大小调整，请仅对所显示的行进行大小调整。  在虚拟模式下也仅调整所显示的行的大小。  
  
    -   对于行和列，使用 <xref:System.Windows.Forms.DataGridViewAutoSizeRowsMode>、<xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode> 和 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode> 枚举的 `DisplayedCells` 或 `DisplayedCellsExceptHeaders` 字段。  
  
    -   对于行标题，使用 <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode> 枚举的 <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode> 或 <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode> 字段。  
  
-   为了获得最大的伸缩性，请关闭自动大小调整并通过编程来重新调整大小。  
  
 有关更多信息，请参见 [Windows 窗体 DataGridView 控件中的大小调整选项](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md)。  
  
## 有效使用选定单元格、行和列的集合  
 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> 集合的执行对于大型选择是低效的。  使用 <xref:System.Windows.Forms.DataGridView.SelectedRows%2A> 和 <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> 集合执行效率也不高，但是程度要轻一些，因为在一个典型的 <xref:System.Windows.Forms.DataGridView> 控件中行远远少于单元格，列远远少于行。  为了避免由于使用以上集合而造成性能下降，请遵循以下准则：  
  
-   若要在访问 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> 集合内容之前确定是否已经在 <xref:System.Windows.Forms.DataGridView> 中选择了所有单元格，请检查 <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A> 方法的返回值。  然而，请注意，此方法可导致行成为非共享行。  有关更多信息，请参见下一节。  
  
-   避免使用 <xref:System.Windows.Forms.DataGridViewSelectedCellCollection?displayProperty=fullName> 的 <xref:System.Collections.ICollection.Count%2A> 属性确定所选单元格的数量。  而是使用 <xref:System.Windows.Forms.DataGridView.GetCellCount%2A?displayProperty=fullName> 方法并传入 <xref:System.Windows.Forms.DataGridViewElementStates?displayProperty=fullName> 值。  同样，可使用 <xref:System.Windows.Forms.DataGridViewRowCollection.GetRowCount%2A?displayProperty=fullName> 和 <xref:System.Windows.Forms.DataGridViewColumnCollection.GetColumnCount%2A?displayProperty=fullName> 方法来确定所选元素的数量，而不是通过访问所选行和列的集合来确定。  
  
-   避免基于单元格的选择模式。  应将 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=fullName> 属性设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode?displayProperty=fullName> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode?displayProperty=fullName>。  
  
## 使用共享行  
 在 <xref:System.Windows.Forms.DataGridView> 控件中可通过共享行实现内存的高效使用。  通过共享 <xref:System.Windows.Forms.DataGridViewRow> 类的实例，行将共享尽可能多的有关自身外观和行为的信息。  
  
 虽然共享行实例节省内存，但是行很容易成为非共享行。  例如，每当用户直接同单元格进行交互时，单元格的行成为非共享行。  由于这是不能避免的，所以仅当处理大量数据，以及仅当用户在运行您的程序时与相对少的部分数据进行交互的情况下，本主题中的准则才是有用的。  
  
 如果行中的任意单元格包含值，在未绑定的 <xref:System.Windows.Forms.DataGridView> 控件中不能共享行。  当 <xref:System.Windows.Forms.DataGridView> 控件绑定到外部数据源或当您实现虚拟模式并且提供自己的数据源时，单元格的值被存储在控件外而不是单元格对象中，因而允许行共享。  
  
 仅当行中所有单元格的状态可以由包含这些单元格的行状态和列状态确定时，行对象才能共享。  如果您更改单元格状态以使其不再派生自所处行和列的状态，则不能共享行。  
  
 例如，在下列任何情况均不能共享行：  
  
-   行包含一个不在所选列中的选定的单元格。  
  
-   行包含一个设置了 <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A> 或 <xref:System.Windows.Forms.DataGridViewCell.ContextMenuStrip%2A> 属性的单元格。  
  
-   行包含一个设置了 <xref:System.Windows.Forms.DataGridViewComboBoxCell.Items%2A> 属性的 <xref:System.Windows.Forms.DataGridViewComboBoxCell>。  
  
 在绑定模式或虚拟模式中，您可以通过处理 <xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded> 和 <xref:System.Windows.Forms.DataGridView.CellContextMenuStripNeeded> 事件为每个单元格提供 工具提示和快捷菜单。  
  
 每当向 <xref:System.Windows.Forms.DataGridViewRowCollection> 添加行时，<xref:System.Windows.Forms.DataGridView> 控件将自动尝试使用共享行。  为确保行被共享，请遵循以下准则：  
  
-   避免调用 <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=fullName> 集合的 <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A> 方法的 `Add(Object[])` 重载和 <xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A> 方法的 `Insert(Object[])` 重载。  以上重载自动创建非共享行。  
  
-   请确保在 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A?displayProperty=fullName> 属性中指定的行可以在以下情况中共享：  
  
    -   当调用 <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=fullName> 集合的 <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A> 方法的 `Add()` 或 `Add(Int32)` 重载或 <xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A> 方法的 `Insert(Int32,Int32)` 重载时。  
  
    -   当增大 <xref:System.Windows.Forms.DataGridView.RowCount%2A?displayProperty=fullName> 属性的值时。  
  
    -   当设置 <xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=fullName> 属性时。  
  
-   请确保在调用 <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=fullName> 集合的 <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopy%2A>、<xref:System.Windows.Forms.DataGridViewRowCollection.AddCopies%2A>、<xref:System.Windows.Forms.DataGridViewRowCollection.InsertCopy%2A> 和 <xref:System.Windows.Forms.DataGridViewRowCollection.InsertCopies%2A> 方法时可以共享 `indexSource` 参数指定的行。  
  
-   请确保在调用 <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=fullName> 集合的 <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A> 方法的 `Add(DataGridViewRow)` 重载、<xref:System.Windows.Forms.DataGridViewRowCollection.AddRange%2A> 方法、<xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A> 方法的 `Insert(Int32,DataGridViewRow)` 重载以及 <xref:System.Windows.Forms.DataGridViewRowCollection.InsertRange%2A> 方法时可以共享指定的行。  
  
 若要确定行是否共享，请使用 <xref:System.Windows.Forms.DataGridViewRowCollection.SharedRow%2A?displayProperty=fullName> 方法检索行对象，然后检查该对象的 <xref:System.Windows.Forms.DataGridViewBand.Index%2A> 属性。  共享行的 <xref:System.Windows.Forms.DataGridViewBand.Index%2A> 属性值始终为 –1。  
  
## 防止行成为非共享行  
 共享行可以由于程序代码或用户操作而成为非共享行。  为了避免对性能的影响，您应该避免使行成为非共享行。  在应用程序开发过程中，可以处理 <xref:System.Windows.Forms.DataGridView.RowUnshared> 事件来确定行何时成为非共享行。  这在调试行共享问题时十分有用。  
  
 若要防止行成为非共享行，请遵循以下准则：  
  
-   避免对 <xref:System.Windows.Forms.DataGridView.Rows%2A> 集合进行索引或者避免使用 `foreach` 循环通过该集合进行迭代。  您通常不需要直接访问行。  对行进行操作的 <xref:System.Windows.Forms.DataGridView> 方法以行索引而不是行实例作为参数。  另外，与行相关的事件的处理程序接收具有行属性的事件参数对象，您可以使用行属性对行执行操作，而不会使行变为非共享行。  
  
-   如果需要访问行对象，请使用 <xref:System.Windows.Forms.DataGridViewRowCollection.SharedRow%2A?displayProperty=fullName> 方法并传入行的实际索引。  然而，请注意，修改一个通过此方法检索的共享行对象将修改所有共享该对象的行。  但是，新记录行不与其他行共享，因此当修改任意其他行时不会影响新记录行。  还应该注意到由一个共享行表示的不同的行可能有不同的快捷菜单。  若要从一个被共享的行实例中检索正确的快捷菜单，请使用 <xref:System.Windows.Forms.DataGridViewRow.GetContextMenuStrip%2A> 方法并传入行的实际索引。  如果您访问共享行的 <xref:System.Windows.Forms.DataGridViewRow.ContextMenuStrip%2A> 属性，它将使用共享行的索引值 \-1 并且不检索正确的快捷菜单。  
  
-   避免对 <xref:System.Windows.Forms.DataGridViewRow.Cells%2A?displayProperty=fullName> 集合进行索引。  直接访问单元格将导致其父行成为非共享行，从而实例化一个新的 <xref:System.Windows.Forms.DataGridViewRow>。  与单元格相关的事件的处理程序接收具有单元格属性的事件参数对象，您可以使用行属性对行执行操作，而不会使行变为非共享行。  也可以使用 <xref:System.Windows.Forms.DataGridView.CurrentCellAddress%2A> 属性，在无需直接访问单元格的情况下检索当前单元格的行和列索引。  
  
-   避免基于单元格的选择模式。  这些模式可导致行成为非共享行。  应将 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=fullName> 属性设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode?displayProperty=fullName> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode?displayProperty=fullName>。  
  
-   不要处理 <xref:System.Windows.Forms.DataGridViewRowCollection.CollectionChanged?displayProperty=fullName> 或 <xref:System.Windows.Forms.DataGridView.RowStateChanged?displayProperty=fullName> 事件。  这些事件可导致行成为非共享行。  也不要调用引发这些事件的 <xref:System.Windows.Forms.DataGridViewRowCollection.OnCollectionChanged%2A?displayProperty=fullName> 或 <xref:System.Windows.Forms.DataGridView.OnRowStateChanged%2A?displayProperty=fullName> 方法。  
  
-   当 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=fullName> 属性值是 <xref:System.Windows.Forms.DataGridViewSelectionMode>、<xref:System.Windows.Forms.DataGridViewSelectionMode>、<xref:System.Windows.Forms.DataGridViewSelectionMode> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode> 时，不要访问 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A?displayProperty=fullName> 集合。  这会导致所有选中行成为非共享行。  
  
-   不要调用 <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A?displayProperty=fullName> 方法。  此方法会导致行成为非共享行。  
  
-   当 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=fullName> 属性值是 <xref:System.Windows.Forms.DataGridViewSelectionMode> 时，不要调用 <xref:System.Windows.Forms.DataGridView.SelectAll%2A?displayProperty=fullName> 方法。  这会导致所有行成为非共享行。  
  
-   当单元格列的相应属性设置为 `true` 时，不要将单元格的 <xref:System.Windows.Forms.DataGridViewCell.ReadOnly%2A> 或 <xref:System.Windows.Forms.DataGridViewCell.Selected%2A> 属性设置为 `false`。  这会导致所有行成为非共享行。  
  
-   不要访问 <xref:System.Windows.Forms.DataGridViewRowCollection.List%2A?displayProperty=fullName> 属性。  这会导致所有行成为非共享行。  
  
-   不要调用 <xref:System.Windows.Forms.DataGridView.Sort%2A> 方法的 `Sort(IComparer)` 重载。  使用自定义比较器排序可导致所有行成为非共享行。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 [Windows 窗体 DataGridView 控件中的性能优化](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的虚拟模式](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的数据显示模式](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [如何：设置 Windows 窗体 DataGridView 控件的默认单元格样式](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的大小调整选项](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md)