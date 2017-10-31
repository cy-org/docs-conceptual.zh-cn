---
title: "Windows 窗体 DataGridView 控件中的数据显示模式 | Microsoft Docs"
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
  - "数据 [Windows 窗体], 显示模式"
  - "数据网格, 显示模式"
  - "DataGridView 控件 [Windows 窗体], 显示模式"
ms.assetid: 9755a030-3f3f-4705-a661-ba5a48a81875
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Windows 窗体 DataGridView 控件中的数据显示模式
<xref:System.Windows.Forms.DataGridView> 控件可以三种不同的模式显示数据：绑定、未绑定和虚拟。  可根据需要选择最合适的模式。  
  
## 未绑定  
 未绑定模式适合于显示由程序管理的相对较少量的数据。  您不会象绑定模式那样将 <xref:System.Windows.Forms.DataGridView> 控件直接连接到数据源。  相反，您必须亲自填充该控件，通常是使用 <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A?displayProperty=fullName> 方法。  
  
 未绑定模式对于静态只读数据非常有用，或者当您希望提供自己的与外部数据存储区进行交互的代码，该模式同样非常有用。  但如果您希望您的用户与外部数据源进行交互，则通常使用绑定模式。  
  
 有关使用只读的未绑定 <xref:System.Windows.Forms.DataGridView> 的示例，请参见 [如何：创建未绑定的 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/how-to-create-an-unbound-windows-forms-datagridview-control.md)。  
  
## 绑定  
 绑定模式适合于使用与数据存储区的自动交互来管理数据。  通过设置 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 属性，可将 <xref:System.Windows.Forms.DataGridView> 控件直接连接到其数据源。  当该控件绑定到数据时，无需您的主动管理即可存入和提取数据行。  当 <xref:System.Windows.Forms.DataGridView.AutoGenerateColumns%2A> 属性为 `true` 时，将在控件中为数据源中的每一列创建相对应的列。  如果您希望创建自己的列，则可将此属性设置为 `false`，并在配置列时使用 <xref:System.Windows.Forms.DataGridViewColumn.DataPropertyName%2A> 属性绑定每一列。  当您想使用的列类型不是默认生成的类型时，此功能将非常有用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件中的列类型](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)。  
  
 有关使用绑定的 <xref:System.Windows.Forms.DataGridView> 控件的示例，请参见 [演练：验证 Windows 窗体 DataGridView 控件中的数据](../../../../docs/framework/winforms/controls/walkthrough-validating-data-in-the-windows-forms-datagridview-control.md)。  
  
 也可以将未绑定列添加到使用绑定模式的 <xref:System.Windows.Forms.DataGridView> 控件。  当希望显示一列使用户能对特定行执行操作的按钮或链接时，此功能将会非常有用。  有时需要显示其值由绑定列计算得出的列。  可以在 <xref:System.Windows.Forms.DataGridView.CellFormatting> 事件的处理程序中填充计算列的单元格值。  但如果是使用 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 作为数据源，则可能需要改用 <xref:System.Data.DataColumn.Expression%2A?displayProperty=fullName> 属性来创建计算列。  在此情况下，<xref:System.Windows.Forms.DataGridView> 控件将象处理数据源中所有其他列那样处理计算列。  
  
 在绑定模式下按未绑定列进行排序不受支持。  如果在绑定模式下创建包含用户可编辑值的未绑定列，则必须实现虚拟模式以便在按绑定列对控件进行排序时保留这些值。  
  
## Virtual  
 使用虚拟模式，您可以实现自己的数据管理操作。  当处于绑定模式时，为了能够在按绑定列对控件进行排序时保留未绑定列的值，此模式是必需的。  但是，虚拟模式的主要用途是在与大量数据进行交互时优化性能。  
  
 您将 <xref:System.Windows.Forms.DataGridView> 控件连接到您所管理的缓存，而您的代码控制何时存入和提取数据行。  若要使内存占有量保持较低水平，缓存大小应与当前所显示的行数相当。  当用户将新行滚入视图中时，代码从缓存请求新的数据，并且可选择将旧数据从内存删除。  
  
 在实现虚拟模式时，您需要跟踪数据模型中何时需要新行，以及何时回滚新行的添加操作。  此项功能能否完全实现将取决于数据模型的实现以及数据模型的事务语义；还有，提交范围是在单元格级还是行级。  
  
 有关虚拟模式的更多信息，请参见 [Windows 窗体 DataGridView 控件中的虚拟模式](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md)。  有关显示如何使用虚拟模式事件的示例，请参见 [演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.Windows.Forms.DataGridViewColumn.DataPropertyName%2A?displayProperty=fullName>   
 [在 Windows 窗体 DataGridView 控件中显示数据](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的列类型](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)   
 [演练：创建未绑定的 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/walkthrough-creating-an-unbound-windows-forms-datagridview-control.md)   
 [如何：将数据绑定到 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/how-to-bind-data-to-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的虚拟模式](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md)   
 [演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)