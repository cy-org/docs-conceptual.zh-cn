---
title: "如何：使用设计器设置 Windows 窗体 DataGridView 控件的默认单元格样式和数据格式 | Microsoft Docs"
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
  - "单元格, 设置样式"
  - "数据 [Windows 窗体], 设置格式"
  - "数据格式"
  - "DataGridView 控件 [Windows 窗体], 单元格样式"
ms.assetid: fc6da49f-8942-41da-b49f-b2afc38cc656
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：使用设计器设置 Windows 窗体 DataGridView 控件的默认单元格样式和数据格式
通过 <xref:System.Windows.Forms.DataGridView> 控件可指定整个控件、某些特定列、行和列标头以及交替行的默认单元格样式和单元格数据格式，从而产生帐目型效果。  为列和交替行设置的默认样式会取代为整个控件设置的默认样式。  此外，在代码中为个别行和单元格设置的样式会取代默认样式。  
  
 有关单元格样式的更多信息，请参见 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)。  若要设置交替行的样式，请参见 [如何：使用设计器设置 Windows 窗体 DataGridView 控件的交替行样式](../../../../docs/framework/winforms/controls/set-alternating-row-styles-for-the-datagrid-using-the-designer.md)。  
  
 也可使用 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A> 属性设置样式，这样做会对所有将要添加到控件中的行产生影响。  有关行模板的更多信息，请参见 [如何：使用行模板自定义 Windows 窗体 DataGridView 控件中的行](../../../../docs/framework/winforms/controls/use-the-row-template-to-customize-rows-in-the-datagrid.md)。  
  
 下面的过程要求有一个带窗体的**“Windows 应用程序”**项目，且窗体中要包括一个 <xref:System.Windows.Forms.DataGridView> 控件。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 设置控件中所有单元格的默认样式  
  
1.  在设计器中选择 <xref:System.Windows.Forms.DataGridView> 控件。  
  
2.  在**“属性”**窗口中，单击 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A>、<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> 或 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A> 属性旁的省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)。  **“CellStyle 生成器”**对话框出现。  
  
3.  通过设置这些属性定义样式，并使用**“预览”**窗格确认所做选择。  
  
> [!NOTE]
>  如果启用了可视化样式，行和列标头（除 <xref:System.Windows.Forms.DataGridView.TopLeftHeaderCell%2A> 外）会按当前主题自动调整样式，取代 <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> 和 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A> 属性值。  
>   
>  可使用设计器为多个选定的 <xref:System.Windows.Forms.DataGridView> 控件设置单元格样式，但仅在这些控件中您要修改的单元格样式属性值完全相同时才可这样做。  对于该属性，如果任一单元格样式有所不同，**“CellStyle 生成器”**对话框的**“属性”**窗口将变为空白。  
  
### 设置个别列中的单元格的默认样式  
  
1.  在设计器中右击 <xref:System.Windows.Forms.DataGridView> 控件并选择**“编辑列”**。  
  
2.  从**“选定的列”**列表中选择一列。  
  
3.  在**“列属性”**网格中，单击 <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A> 属性旁的省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)。  **“CellStyle 生成器”**对话框出现。  
  
4.  通过设置这些属性定义样式，并使用**“预览”**窗格确认所做选择。  
  
### 设定单元格中的数据的格式  
  
1.  使用前面的过程之一显示与默认单元格样式属性关联的**“CellStyle 生成器”**对话框。  
  
2.  在**“CellStyle 生成器”**对话框中，单击 <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> 属性旁的省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)。  **“格式字符串”**对话框出现。  
  
3.  选择一个格式类型，然后修改该类型的细节（如要显示的小数位数），并使用**“示例”**框确认所做选择。  
  
4.  如果要将 <xref:System.Windows.Forms.DataGridView> 绑定到可能含 null 值的数据源，请填写**“Null”**文本框。  当单元格值等于 null 引用（Visual Basic 中为 `Nothing`）或 <xref:System.DBNull.Value?displayProperty=fullName> 时，将显示所填写的值。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A?displayProperty=fullName>   
 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [如何：使用设计器设置 Windows 窗体 DataGridView 控件的交替行样式](../../../../docs/framework/winforms/controls/set-alternating-row-styles-for-the-datagrid-using-the-designer.md)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)