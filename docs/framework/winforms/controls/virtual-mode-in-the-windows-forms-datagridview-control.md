---
title: "Windows 窗体 DataGridView 控件中的虚拟模式 | Microsoft Docs"
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
  - "DataGridView 控件 [Windows 窗体], 虚拟模式"
ms.assetid: feae5d43-2848-4b1a-8ea7-77085dc415b5
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Windows 窗体 DataGridView 控件中的虚拟模式
在虚拟模式下，您可以管理 <xref:System.Windows.Forms.DataGridView> 控件和自定义数据缓存之间的交互。  若要实现虚拟模式，请将 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性设置为 `true`，并处理本主题中介绍的一个或多个事件。  您通常至少要处理 `CellValueNeeded` 事件，该事件使控件能够在数据缓存中查找值。  
  
## 绑定模式和虚拟模式  
 仅在需要补充或替换绑定模式时才需要虚拟模式。  在绑定模式下，您可以设置 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 属性，控件会从指定的数据源自动加载数据，并将用户更改提交到该数据源。  您可以就显示哪个绑定列进行控制，数据源通常会自行处理排序等操作。  
  
## 补充绑定模式  
 您可以随绑定列一起显示未绑定列，从而对绑定模式进行补充。  这有时也称为“混合模式”，这种模式在显示计算值或用户界面 \(UI\) 控件时十分有用。  
  
 因为未绑定列位于数据源外，所以会被数据源的排序操作忽略。  因此，当您在混合模式下启用排序时，必须管理本地缓存中的未绑定数据，并实施虚拟模式以使 <xref:System.Windows.Forms.DataGridView> 控件能与这些数据进行交互。  
  
 有关使用虚拟模式维护未绑定列中的值的更多信息，请参见 <xref:System.Windows.Forms.DataGridViewCheckBoxColumn.ThreeState%2A?displayProperty=fullName> 属性和 <xref:System.Windows.Forms.DataGridViewComboBoxColumn?displayProperty=fullName> 类参考主题中的示例。  
  
## 替换绑定模式  
 如果绑定模式无法满足性能要求，则可通过虚拟模式事件处理程序管理自定义缓存中的所有数据。  例如，您可以使用虚拟模式实现一个实时数据加载机制，该机制仅从联网数据库检索必需的数据，以获得最佳的性能。  当通过速度很慢的网络连接或使用 RAM 或存储空间有限的客户端计算机处理大量数据时，此方案特别有用。  
  
 有关在实时方案中使用虚拟模式的更多信息，请参见 [在 Windows 窗体 DataGridView 控件中实现实时数据加载的虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)。  
  
## 虚拟模式事件  
 如果数据是只读的，则 `CellValueNeeded` 事件可能是唯一一个需要处理的事件。  使用其他的虚拟模式事件可以启用特定的功能，如用户编辑、行的添加和删除以及行级事务。  
  
 有些标准 <xref:System.Windows.Forms.DataGridView> 事件在虚拟模式下也很有用，例如在用户添加或删除行时发生的事件，以及在编辑、分析、验证或格式化单元格值时发生的事件。  您还可以处理一些事件来维护通常不存储在绑定数据源中的值，例如单元格工具提示文本、单元格和行错误文本、单元格和行快捷菜单数据以及行高数据。  
  
 有关实现虚拟模式以管理具有行级提交范围的读\/写数据的更多信息，请参见 [演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)。  
  
 有关实现具有单元格级提交范围的虚拟模式的示例，请参见 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性参考主题。  
  
 以下事件仅在 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性设置为 `true` 时发生。  
  
|Event|说明|  
|-----------|--------|  
|<xref:System.Windows.Forms.DataGridView.CellValueNeeded>|由控件用来从数据缓存检索单元格值以进行显示。  此事件仅对未绑定列中的单元格发生。|  
|<xref:System.Windows.Forms.DataGridView.CellValuePushed>|由控件用来将单元格中的用户输入提交到数据缓存。  此事件仅对未绑定列中的单元格发生。<br /><br /> 在从 <xref:System.Windows.Forms.DataGridView.CellValuePushed> 事件处理程序外更改缓存的值时，请调用 <xref:System.Windows.Forms.DataGridView.UpdateCellValue%2A> 方法以确保将当前值显示在控件中并应用当前有效的所有自动的大小调整模式。|  
|<xref:System.Windows.Forms.DataGridView.NewRowNeeded>|由控件用来指示数据缓存中需要新行。|  
|<xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>|由控件用来确定行中是否有任何未提交的更改。|  
|<xref:System.Windows.Forms.DataGridView.CancelRowEdit>|由控件用来指示一个行应恢复为它的缓存的值。|  
  
 以下事件在虚拟模式下十分有用，但无论 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性设置如何都可使用。  
  
|事件|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.DataGridView.UserDeletingRow><br /><br /> <xref:System.Windows.Forms.DataGridView.UserDeletedRow><br /><br /> <xref:System.Windows.Forms.DataGridView.RowsRemoved><br /><br /> <xref:System.Windows.Forms.DataGridView.RowsAdded>|由控件用来指示在何时删除或添加行，使您可以相应地更新数据缓存。|  
|<xref:System.Windows.Forms.DataGridView.CellFormatting><br /><br /> <xref:System.Windows.Forms.DataGridView.CellParsing><br /><br /> <xref:System.Windows.Forms.DataGridView.CellValidating><br /><br /> <xref:System.Windows.Forms.DataGridView.CellValidated><br /><br /> <xref:System.Windows.Forms.DataGridView.RowValidating><br /><br /> <xref:System.Windows.Forms.DataGridView.RowValidated>|由控件用来设置要显示的单元格值的格式以及分析和验证用户输入。|  
|<xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded>|由控件用来在设置了 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 属性或者 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性为 `true` 时检索单元格工具提示文本。<br /><br /> 单元格工具提示仅在 <xref:System.Windows.Forms.DataGridView.ShowCellToolTips%2A> 属性值为 `true` 时显示。|  
|<xref:System.Windows.Forms.DataGridView.CellErrorTextNeeded><br /><br /> <xref:System.Windows.Forms.DataGridView.RowErrorTextNeeded>|由控件用来在设置了 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 属性或者 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性为 `true` 时检索单元格或行的错误文本。<br /><br /> 在更改单元格或行的错误文本时，请调用 <xref:System.Windows.Forms.DataGridView.UpdateCellErrorText%2A> 方法或 <xref:System.Windows.Forms.DataGridView.UpdateRowErrorText%2A> 方法，以确保在控件中显示当前值。<br /><br /> 当 <xref:System.Windows.Forms.DataGridView.ShowCellErrors%2A> 和 <xref:System.Windows.Forms.DataGridView.ShowRowErrors%2A> 属性值为 `true` 时，将显示单元格和行的错误标志符号。|  
|<xref:System.Windows.Forms.DataGridView.CellContextMenuStripNeeded><br /><br /> <xref:System.Windows.Forms.DataGridView.RowContextMenuStripNeeded>|由控件用来在设置了控件的 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 属性或者 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性为 `true` 时检索单元格或行的 <xref:System.Windows.Forms.ContextMenuStrip>。|  
|<xref:System.Windows.Forms.DataGridView.RowHeightInfoNeeded><br /><br /> <xref:System.Windows.Forms.DataGridView.RowHeightInfoPushed>|由控件用来在数据缓存中检索或存储行的高度信息。  在从 <xref:System.Windows.Forms.DataGridView.RowHeightInfoPushed> 事件处理程序外更改缓存的行高信息时，请调用 <xref:System.Windows.Forms.DataGridView.UpdateRowHeightInfo%2A> 方法以确保在控件中显示当前值。|  
  
## 虚拟模式下的最佳做法  
 如果要实现虚拟模式以提高操作大量数据时的效率，则可能还需要确保对 <xref:System.Windows.Forms.DataGridView> 控件本身的有效使用。  有关有效使用单元格样式、自动大小调整、选择以及行共享的更多信息，请参见 [缩放 Windows 窗体 DataGridView 控件的最佳做法](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>   
 [Windows 窗体 DataGridView 控件中的性能优化](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)   
 [缩放 Windows 窗体 DataGridView 控件的最佳做法](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)   
 [演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)   
 [在 Windows 窗体 DataGridView 控件中实现实时数据加载的虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)