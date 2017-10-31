---
title: "Windows 窗体 DataGridView 控件中的大小调整选项 | Microsoft Docs"
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
  - "数据网格, 调整列大小"
  - "数据网格, 调整行大小"
  - "数据网格, 大小调整选项"
  - "DataGridView 控件 [Windows 窗体], 调整列大小"
  - "DataGridView 控件 [Windows 窗体], 调整行大小"
  - "DataGridView 控件 [Windows 窗体], 大小调整选项"
ms.assetid: a5620a9c-0d06-41e3-8934-c25ddb16c9e6
caps.latest.revision: 29
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 29
---
# Windows 窗体 DataGridView 控件中的大小调整选项
在发生很多不同情况时，可以导致 <xref:System.Windows.Forms.DataGridView> 行、列和标题更改大小。  下表显示了这些情况。  
  
|情况|说明|  
|--------|--------|  
|用户调整大小|用户可以通过拖动或双击行、列或标题分隔符来调整大小。|  
|控件调整大小|在列填充模式中，如果控件宽度发生更改，则列宽度将更改；例如，当控件停靠在它的父窗体上和用户调整窗体大小时。|  
|单元格值更改|在基于内容的自动调整大小模式中，大小将为了容纳新的显示值而发生更改。|  
|方法调用|通过编程实现的基于内容的调整大小允许您在发生方法调用时基于单元格值进行随机的大小调整。|  
|属性设置|还可以设置特定的高度和宽度值。|  
  
 默认情况下，将启用用户调整大小、禁用自动调整大小并减小宽度大于其列的单元格值。  
  
 通过使用下表中显示的方案，可以调整默认行为，或使用特定的调整大小选项来获得特定的效果。  
  
|方案|实现|  
|--------|--------|  
|使用列填充模式在占据控件的整个宽度并且个数相对较少的列中显示相似的调整大小数据，而不显示水平滚动条。|将 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>。|  
|对大小变化的显示值使用列填充模式。|将 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>。  在用数据填充控件之后，通过设置列 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 的属性或调用控件的 <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A> 方法来初始化相对的列宽度。|  
|对重要性变化的值使用列填充模式。|将 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>。  对必须始终显示其某些数据的列设置大型 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 值，或对特定列使用填充模式以外的调整大小选项。|  
|使用列填充模式以避免显示控件背景。|将最后一列的 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>，并对其他列使用其他调整大小选项。  如果其他列使用了过多的可用空间，可设置最后一列的 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 属性。|  
|显示固定宽度的列，例如，图标或 ID 列。|将该列的 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> 设置为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>，并将 <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A> 设置为 <xref:System.Windows.Forms.DataGridViewTriState>。  用数据填充控件之后，通过设置 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A> 属性或调用控件的 <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A> 方法来初始化它的宽度。|  
|一旦单元格内容发生更改，则自动调整大小，以避免发生裁减，并优化空间的使用。|将自动调整大小属性设置为可表示基于内容的调整大小模式的值。  若要避免在处理大量数据时性能有损失，请使用只计算所显示的行的调整大小模式。|  
|调整大小以容纳显示行中的值，以避免在处理很多行时性能有损失。|对于自动或编程的调整大小，使用相应的调整大小模式枚举值。  若要调整大小以便在滚动时容纳新显示的行中的值，请在 <xref:System.Windows.Forms.DataGridView.Scroll> 事件处理程序中调用调整大小方法。  若要自定义用户双击时的调整大小，以便仅由显示行中的值来确定新的大小，请在 <xref:System.Windows.Forms.DataGridView.RowDividerDoubleClick> 或 <xref:System.Windows.Forms.DataGridView.ColumnDividerDoubleClick> 事件处理程序中调用调整大小方法。|  
|仅在特定时间调整大小以容纳单元格内容，以避免性能有损失，或启用用户调整大小。|在事件处理程序中调用基于内容的调整大小方法。  例如，使用 <xref:System.Windows.Forms.DataGridView.DataBindingComplete> 事件可以在绑定后初始化大小，并通过处理 <xref:System.Windows.Forms.DataGridView.CellValidated> 或 <xref:System.Windows.Forms.DataGridView.CellValueChanged> 事件以调整大小，从而补偿绑定的数据源中的用户编辑或更改。|  
|调整多行单元格内容的行高。|确保列宽对于显示文本段落是合适的，并使用自动或编程的基于内容的行调整大小来调整高度。  还要确保使用 <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> 单元格样式值 <xref:System.Windows.Forms.DataGridViewTriState> 来显示包含多行内容的单元格。<br /><br /> 通常，将使用自动列调整大小模式来维护列宽，或在调整行高之前将它们设置为特定的宽度。|  
  
## 用鼠标调整大小  
 默认情况下，对于不使用基于单元格值的自动调整大小模式的行、列和标题来说，可以由用户调整它们的大小。  若要防止用户用其他模式（例如，列填充模式）调整大小，请设置一个或多个下面的 <xref:System.Windows.Forms.DataGridView> 属性：  
  
-   <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A>  
  
 还可以通过设置其 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> 属性来防止用户调整单个行或列的大小。  默认情况下，<xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> 属性值基于列的 <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A> 属性值和行的 <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A> 属性值。  但是，如果显式地将 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> 设置为 <xref:System.Windows.Forms.DataGridViewTriState> 或 <xref:System.Windows.Forms.DataGridViewTriState>，则所指定的值将重写针对该行或列的控件值。  将 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> 设置为 <xref:System.Windows.Forms.DataGridViewTriState> 可以还原继承。  
  
 由于 <xref:System.Windows.Forms.DataGridViewTriState> 会还原值继承，因此，除非该行或列尚未添加到 <xref:System.Windows.Forms.DataGridView> 控件中，否则 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> 属性永远不会返回 <xref:System.Windows.Forms.DataGridViewTriState> 值。  如果需要确定是否继承了行或列的 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> 属性值，请检查它的 <xref:System.Windows.Forms.DataGridViewElement.State%2A> 属性。  如果 <xref:System.Windows.Forms.DataGridViewElement.State%2A> 值包括 <xref:System.Windows.Forms.DataGridViewElementStates> 标志，则不继承 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> 属性值。  
  
## 自动调整大小  
 在 <xref:System.Windows.Forms.DataGridView> 控件中有两种自动调整大小：列填充模式和基于内容的自动调整大小。  
  
 列填充模式导致控件中的可见列按控件的显示区域的宽度进行填充。  有关该模式的更多信息，请参见 [Windows 窗体 DataGridView 控件中的列填充模式](../../../../docs/framework/winforms/controls/column-fill-mode-in-the-windows-forms-datagridview-control.md)。  
  
 还可以配置行、列和标题，使其自动调整它们的大小以容纳它们的单元格内容。  在这种情况下，一旦单元格内容发生更改，就会发生大小调整。  
  
> [!NOTE]
>  如果使用虚拟模式在自定义的数据缓存中维护单元格值，则在用户编辑单元格值时发生自动调整大小，但如果在 <xref:System.Windows.Forms.DataGridView.CellValuePushed> 事件处理程序以外更改缓存值时则不发生。  在这种情况下，调用 <xref:System.Windows.Forms.DataGridView.UpdateCellValue%2A> 方法可以强制控件更新单元格的显示，并应用当前的自动调整大小模式。  
  
 如果仅对一个维度（就是说，对行但不对列，或对列但不对行）启用基于内容的自动调整大小，并且还启用了 <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A>，那么一旦其他维度发生更改，也会发生大小调整。  例如，如果为行但没有为列配置自动调整大小，并且启用了 <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A>，则用户可以拖动列分隔符以更改列的宽度，并且行高将自动调整，以便仍然能够完全显示单元格内容。  
  
 如果同时为行和列配置了基于内容的自动调整大小，并且启用了 <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A>，则一旦单元格内容发生更改，<xref:System.Windows.Forms.DataGridView> 控件就将调整大小，并且在计算新大小时，该控件将使用理想的单元格高宽比率。  
  
 若要为标题和行配置调整大小模式，并为未重写此控件值的列配置该模式，请设置一个或多个下面的 <xref:System.Windows.Forms.DataGridView> 属性：  
  
-   <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoSizeRowsMode%2A>  
  
 若要为控件的单个列重写列调整大小模式，请将它的 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> 属性设置为除 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode> 以外的其他值。  实际上，列的调整大小模式由它的 <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A> 属性确定。  此属性的值基于列的 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> 属性值，除非该值是 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>，这种情况下，将继承控件的 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> 值。  
  
 处理大量数据时，如果要使用基于内容的自动调整大小，则要小心。  若要避免性能有损失，请使用自动调整大小模式，该模式将仅基于所显示的行而不会分析控件中的每个行来计算大小。  要获得最高性能，请转而使用编程调整大小，以便可以在特定时间调整大小（例如，在加载新数据之后立即执行）。  
  
 基于内容的自动调整大小模式不会影响通过将行或列的 <xref:System.Windows.Forms.DataGridViewBand.Visible%2A> 属性或将控件的 <xref:System.Windows.Forms.DataGridView.RowHeadersVisible%2A> 或 <xref:System.Windows.Forms.DataGridView.ColumnHeadersVisible%2A> 属性设置为 `false` 而已经隐藏起来的行、列或标题。  例如，如果在自动调整列的大小以容纳大型单元格值之后该列被隐藏，则在删除包含该大型单元格值的行时，该隐藏列不会更改其大小。  当可见性更改时，不会发生自动调整大小，因此，如果将列的 <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A> 属性改回 `true`，将不会强制该列基于其当前内容而重新计算其大小。  
  
 而编程的基于内容的调整大小则会影响行、列和标题，不管它们的可见性如何。  
  
## 编程调整大小  
 如果禁用了自动调整大小，则可以用编程的方式通过下面的属性来为行、列或标题设置准确的宽度或高度：  
  
-   <xref:System.Windows.Forms.DataGridView.RowHeadersWidth%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeight%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.DataGridViewRow.Height%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=fullName>  
  
 还可以使用下面的方法通过编程来调整行、列和标题的大小，使其能够容纳它们的内容：  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeColumnHeadersHeight%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeRow%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeRowHeadersWidth%2A>  
  
 这些方法将一次性调整行、列或标题的大小，而不用为了连续调整大小而配置它们。  系统将自动计算新的大小，以便在不发生裁减的情况下显示所有单元格内容。  但是，如果通过编程来对 <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A> 属性值为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode> 的列进行大小调整，则会用经过计算的基于内容的宽度按比例调整该列的 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 属性值，然后按照这些新的比例计算实际的列宽，以便让所有列填充该控件的可用显示区域。  
  
 编程调整大小可以用来避免连续调整大小时出现性能损失。  它还可用于为可由用户调整大小的行、列和标题以及为列填充模式提供初始大小。  
  
 通常，您将在特定时间调用编程调整大小方法。  例如，可能在加载数据之后立即通过编程来调整所有列的大小，也可能在已修改特定单元格值之后通过编程来调整特定行的大小。  
  
## 自定义基于内容的调整大小行为  
 通过重写 <xref:System.Windows.Forms.DataGridViewCell.GetPreferredSize%2A?displayProperty=fullName>、<xref:System.Windows.Forms.DataGridViewRow.GetPreferredHeight%2A?displayProperty=fullName> 或 <xref:System.Windows.Forms.DataGridViewColumn.GetPreferredWidth%2A?displayProperty=fullName> 方法，或通过在派生的 <xref:System.Windows.Forms.DataGridView> 控件中调用受保护的调整大小方法重载，可以在处理派生的 <xref:System.Windows.Forms.DataGridView> 单元格、行和列类型时自定义调整大小行为。  设计受保护的调整大小方法重载是为了进行成对处理，以便获得理想的单元格高宽比率，从而避免出现过宽或过高的单元格。  例如，如果调用 <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A> 方法的 `AutoResizeRows(DataGridViewAutoSizeRowsMode,Boolean)` 重载，并为 <xref:System.Boolean> 参数传入值 `false`，则该重载将为行中的单元格计算理想的高度和宽度，但是，它只会调整行高。  然后，必须调用 <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A> 方法，才能将列宽调整为计算得到的理想值。  
  
## 基于内容的调整大小选项  
 对于基于内容的调整大小来说，调整大小的属性和方法所使用的枚举有相似的值。  使用这些值，可以限制使用哪些单元格来计算首选的大小。  对于所有调整大小枚举，其名称引用所显示的单元格的值会将其计算范围限制于所显示的行中的单元格。  若要在处理大量行时避免出现性能损失，则排除行将是有用的。  还可以将计算范围限制于标题或非标题单元格中的单元格值。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoSizeRowsMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowHeadersWidth%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeight%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewRow.Height%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumnHeadersHeight%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeRow%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeRowHeadersWidth%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeRowMode>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeRowsMode>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>   
 <xref:System.Windows.Forms.DataGridViewColumnHeadersHeightSizeMode>   
 <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode>   
 [调整 Windows 窗体 DataGridView 控件中列和行的大小](../../../../docs/framework/winforms/controls/resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的列填充模式](../../../../docs/framework/winforms/controls/column-fill-mode-in-the-windows-forms-datagridview-control.md)   
 [如何：设置 Windows 窗体 DataGridView 控件的大小调整模式](../../../../docs/framework/winforms/controls/how-to-set-the-sizing-modes-of-the-windows-forms-datagridview-control.md)