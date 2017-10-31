---
title: "Windows 窗体 DataGridView 控件中的列类型 | Microsoft Docs"
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
  - "列 [Windows 窗体], 类型"
  - "数据网格, 列"
  - "DataGridView 控件 [Windows 窗体], 列类型"
ms.assetid: f0a0a9f1-8757-4bfd-891f-d7d12870dbed
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Windows 窗体 DataGridView 控件中的列类型
<xref:System.Windows.Forms.DataGridView> 控件使用多种列类型显示其信息，并使用户能够修改或添加信息。  
  
 当绑定 <xref:System.Windows.Forms.DataGridView> 控件并将 <xref:System.Windows.Forms.DataGridView.AutoGenerateColumns%2A> 属性设置为 `true` 时，会使用与绑定数据源中包含的数据类型相应的默认列类型自动生成列。  
  
 您也可以自行创建任何列类的实例，并将其添加到由 <xref:System.Windows.Forms.DataGridView.Columns%2A> 属性返回的集合中。  可以创建这些实例以用作未绑定列，也可以手动绑定这些实例。  手动绑定的列十分有用，例如，当您将一种类型的自动生成的列替换为另一种类型的列时，就可以使用手动绑定的列。  
  
 下表介绍可在 <xref:System.Windows.Forms.DataGridView> 控件中使用的各种列类。  
  
|类|说明|  
|-------|--------|  
|<xref:System.Windows.Forms.DataGridViewTextBoxColumn>|与基于文本的值一起使用。  在绑定到数字和字符串时自动生成。|  
|<xref:System.Windows.Forms.DataGridViewCheckBoxColumn>|与 <xref:System.Boolean> 和 <xref:System.Windows.Forms.CheckState> 值一起使用。  在绑定到这些类型的值时自动生成。|  
|<xref:System.Windows.Forms.DataGridViewImageColumn>|用于显示图像。  在绑定到字节数组、<xref:System.Drawing.Image> 对象或 <xref:System.Drawing.Icon> 对象时自动生成。|  
|<xref:System.Windows.Forms.DataGridViewButtonColumn>|用于在单元格中显示按钮。  不会在绑定时自动生成。  通常用作未绑定列。|  
|<xref:System.Windows.Forms.DataGridViewComboBoxColumn>|用于在单元格中显示下拉列表。  不会在绑定时自动生成。  通常手动进行数据绑定。|  
|<xref:System.Windows.Forms.DataGridViewLinkColumn>|用于在单元格中显示链接。  不会在绑定时自动生成。  通常手动进行数据绑定。|  
|自定义列类型|您可以通过继承 <xref:System.Windows.Forms.DataGridViewColumn> 类或该类的任何一个派生类来创建自己的列类，从而提供自定义的外观、行为或寄宿控件。  有关更多信息，请参见 [如何：通过扩展 Windows 窗体 DataGridView 控件中单元格和列的行为和外观对其进行自定义](../../../../docs/framework/winforms/controls/customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md)|  
  
 以下各节将更详细地介绍这些列类型。  
  
## DataGridViewTextBoxColumn  
 <xref:System.Windows.Forms.DataGridViewTextBoxColumn> 是一种通用的列类型，用于基于文本的值，如数字和字符串。  在编辑模式下，<xref:System.Windows.Forms.TextBox> 控件显示在活动单元格中，允许用户修改单元格的值。  
  
 单元格值会自动转换为字符串以供显示。  自动对用户输入或修改的值进行分析，以创建具有相应数据类型的单元格值。  可以通过处理 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.CellFormatting> 和 <xref:System.Windows.Forms.DataGridView.CellParsing> 事件自定义这些转换。  
  
 某一列的单元格值数据类型在该列的 <xref:System.Windows.Forms.DataGridViewColumn.ValueType%2A> 属性中指定。  
  
## DataGridViewCheckBoxColumn  
 <xref:System.Windows.Forms.DataGridViewCheckBoxColumn> 可与 <xref:System.Boolean> 和 <xref:System.Windows.Forms.CheckState> 值一起使用。  <xref:System.Boolean> 值显示为具有两个或三个状态的复选框，具体取决于 <xref:System.Windows.Forms.DataGridViewCheckBoxColumn.ThreeState%2A> 属性的值。  当该列绑定到 <xref:System.Windows.Forms.CheckState> 值时，默认情况下 <xref:System.Windows.Forms.DataGridViewCheckBoxColumn.ThreeState%2A> 属性的值为 `true`。  
  
 通常情况下，复选框单元格值要么像其他数据一样用于存储，要么用于执行批量操作。  如果您想在用户单击复选框单元格时立即作出响应，可以处理 <xref:System.Windows.Forms.DataGridView.CellClick> 事件，但此事件发生在单元格值更新之前。  如果在单击时需要新的值，则有一个选项可以计算基于当前值的预期值。  另一种方法是立即提交更改，并处理 <xref:System.Windows.Forms.DataGridView.CellValueChanged> 事件以对此作出响应。  要在单击单元格时提交更改，必须处理 <xref:System.Windows.Forms.DataGridView.CurrentCellDirtyStateChanged> 事件。  在处理程序中，如果当前单元格是复选框单元格，则调用 <xref:System.Windows.Forms.DataGridView.CommitEdit%2A> 方法并传入 <xref:System.Windows.Forms.DataGridViewDataErrorContexts> 值。  
  
## DataGridViewImageColumn  
 <xref:System.Windows.Forms.DataGridViewImageColumn> 用于显示图像。  图像列可从数据源自动填充，可针对未绑定列手动填充，也可使用 <xref:System.Windows.Forms.DataGridView.CellFormatting> 事件的处理程序动态填充。  
  
 从数据源自动填充图像列时可使用各种图像格式的字节数组，包括 <xref:System.Drawing.Image> 类支持的所有格式以及 Microsoft® Access 和 Northwind 示例数据库使用的 OLE 图片格式。  
  
 如果要提供 <xref:System.Windows.Forms.DataGridViewButtonColumn> 的功能而又要使用自定义的外观，则可手动填充图像列。  可以处理 <xref:System.Windows.Forms.DataGridView.CellClick?displayProperty=fullName> 事件，以响应图像单元格中的单击。  
  
 如果要为计算得出的值或非图像格式的值提供图像，可使用 <xref:System.Windows.Forms.DataGridView.CellFormatting> 事件的处理程序填充图像列中的单元格。  例如，您可能有一个“Risk”列，并且您希望将其包含的 `"high"`、`"middle"` 和 `"low"` 字符串值显示为图标。  此外，您还可能有一个“Image”列，其中包含必须加载的图像的位置，而不是这些图像的二进制内容。  
  
## DataGridViewButtonColumn  
 使用 <xref:System.Windows.Forms.DataGridViewButtonColumn>，可以显示一列包含按钮的单元格。  如果您希望提供一种简易方式以供用户对特定记录执行操作（如：下订单或在单独的窗口中显示子记录），则此列类型很有用。  
  
 对 <xref:System.Windows.Forms.DataGridView> 控件进行数据绑定时，不会自动生成按钮列。  若要使用按钮列，必须手动创建这些列，并将其添加到 <xref:System.Windows.Forms.DataGridView.Columns%2A?displayProperty=fullName> 属性返回的集合中。  
  
 通过处理 <xref:System.Windows.Forms.DataGridView.CellClick?displayProperty=fullName> 事件，可以响应用户在按钮单元格中的单击。  
  
## DataGridViewComboBoxColumn  
 使用 <xref:System.Windows.Forms.DataGridViewComboBoxColumn>，可以显示一列包含下拉列表框的单元格。  此列类型可用于以下字段中的数据输入，这些字段只能包含某些特定的值，如 Northwind 示例数据库中 Products 表的 Category 列。  
  
 可以采用填充 <xref:System.Windows.Forms.ComboBox> 下拉列表的方式填充用于所有单元格的下拉列表，既可以通过 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.Items%2A> 属性返回的集合手动填充，也可以通过 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DataSource%2A>、<xref:System.Windows.Forms.DataGridViewComboBoxColumn.DisplayMember%2A> 和 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A> 属性将要填充的下拉列表绑定到某个数据源。  有关更多信息，请参见 [ComboBox 控件](../../../../docs/framework/winforms/controls/combobox-control-windows-forms.md)。  
  
 通过设置 <xref:System.Windows.Forms.DataGridViewComboBoxColumn?displayProperty=fullName> 的 <xref:System.Windows.Forms.DataGridViewColumn.DataPropertyName%2A> 属性，可以将实际的单元格值绑定到 <xref:System.Windows.Forms.DataGridView> 控件使用的数据源。  
  
 对 <xref:System.Windows.Forms.DataGridView> 控件进行数据绑定时，不会自动生成组合框列。  若要使用组合框列，必须手动创建这些列，并将其添加到 <xref:System.Windows.Forms.DataGridView.Columns%2A> 属性返回的集合中。  
  
## DataGridViewLinkColumn  
 使用 <xref:System.Windows.Forms.DataGridViewLinkColumn>，可以显示一列包含超链接的单元格。  此列类型可用于数据源中的 URL 值，也可替代用于特殊行为（如打开带有子记录的窗口）的按钮列。  
  
 对 <xref:System.Windows.Forms.DataGridView> 控件进行数据绑定时，不会自动生成链接列。  若要使用链接列，则必须手动创建这些列，并将其添加到 <xref:System.Windows.Forms.DataGridView.Columns%2A> 属性返回的集合中。  
  
 通过处理 <xref:System.Windows.Forms.DataGridView.CellContentClick> 事件，可以响应用户在链接上的单击。  此事件与用户在单元格中的任何位置单击时出现的 <xref:System.Windows.Forms.DataGridView.CellClick> 和 <xref:System.Windows.Forms.DataGridView.CellMouseClick> 事件不同。  
  
 <xref:System.Windows.Forms.DataGridViewLinkColumn> 类提供了多个属性，用于在单击链接时、单击链接之前和之后修改链接的外观。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn>   
 <xref:System.Windows.Forms.DataGridViewButtonColumn>   
 <xref:System.Windows.Forms.DataGridViewCheckBoxColumn>   
 <xref:System.Windows.Forms.DataGridViewComboBoxColumn>   
 <xref:System.Windows.Forms.DataGridViewImageColumn>   
 <xref:System.Windows.Forms.DataGridViewTextBoxColumn>   
 <xref:System.Windows.Forms.DataGridViewLinkColumn>   
 [DataGridView 控件](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)   
 [如何：在 Windows 窗体 DataGridView 控件的单元格中显示图像](../../../../docs/framework/winforms/controls/how-to-display-images-in-cells-of-the-windows-forms-datagridview-control.md)   
 [如何：使用 Windows 窗体 DataGridView 控件中的图像列](../../../../docs/framework/winforms/controls/how-to-work-with-image-columns-in-the-windows-forms-datagridview-control.md)   
 [自定义 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)