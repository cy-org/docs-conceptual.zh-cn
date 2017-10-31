---
title: "演练：创建未绑定的 Windows 窗体 DataGridView 控件 | Microsoft Docs"
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
  - "数据 [Windows 窗体], 不绑定到数据源显示"
  - "数据 [Windows 窗体], 未绑定"
  - "DataGridView 控件 [Windows 窗体], 不绑定到数据源显示数据"
  - "DataGridView 控件 [Windows 窗体], 未绑定数据"
  - "演练 [Windows 窗体], DataGridView 控件"
ms.assetid: 5a8d6afa-1b4b-4b24-8db8-501086ffdebe
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 演练：创建未绑定的 Windows 窗体 DataGridView 控件
您可能经常需要显示并非来自数据库的表格数据。  例如，您可能要显示一个二维字符串数组的内容。  <xref:System.Windows.Forms.DataGridView> 类提供一种在不绑定到数据源的情况下显示数据的方法，此方法既简单，又具有非常强的可自定义性。  本演练演示如何在“取消绑定”模式下填充 <xref:System.Windows.Forms.DataGridView> 控件以及管理行的添加和删除。  默认情况下，用户可以添加新行。  要禁止添加行，应将 <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> 属性设置为 `false`。  
  
 若要以单个列表的形式复制本主题中的代码，请参见 [如何：创建未绑定的 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/how-to-create-an-unbound-windows-forms-datagridview-control.md)。  
  
## 创建窗体  
  
#### 使用未绑定的 DataGridView 控件  
  
1.  创建一个从 <xref:System.Windows.Forms.Form> 派生并包含下列变量声明和 `Main` 方法的类。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#01](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#01)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#01](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#01)]  
    [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#02](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#02](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#02)]  
  
2.  在窗体的类定义中实现一个 `SetupLayout` 方法以设置窗体的布局。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#20)]  
  
3.  创建一个 `SetupDataGridView` 方法以设置 <xref:System.Windows.Forms.DataGridView> 的列和属性。  
  
     此方法首先向窗体的 <xref:System.Windows.Forms.Control.Controls%2A> 集合中添加 <xref:System.Windows.Forms.DataGridView> 控件。  接下来，使用 <xref:System.Windows.Forms.DataGridView.ColumnCount%2A> 属性设置要显示的列数。  列标题的默认样式是通过设置 <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> 属性返回的 <xref:System.Windows.Forms.DataGridViewCellStyle> 的 <xref:System.Windows.Forms.DataGridViewCellStyle.BackColor%2A>、<xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> 和 <xref:System.Windows.Forms.DataGridViewCellStyle.Font%2A> 属性来设置的。  
  
     布局和外观属性设置好后，接下来该分配列名了。  此方法退出后，便可以填充 <xref:System.Windows.Forms.DataGridView> 控件了。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#30)]  
  
4.  创建一个 `PopulateDataGridView` 方法以便向 <xref:System.Windows.Forms.DataGridView> 控件中添加行。  
  
     每一行都表示一首歌曲及其关联信息。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#40](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#40)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#40](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#40)]  
  
5.  实用工具方法创建好后，便可以开始附加事件处理程序了。  
  
     您将处理**“添加”**和**“删除”**按钮的 <xref:System.Windows.Forms.Control.Click> 事件、窗体的 <xref:System.Windows.Forms.Form.Load> 事件以及 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.CellFormatting> 事件。  
  
     当**“添加”**按钮的 <xref:System.Windows.Forms.Control.Click> 事件引发时，会向 <xref:System.Windows.Forms.DataGridView> 中添加一个新的空行。  
  
     当**“删除”**按钮的 <xref:System.Windows.Forms.Control.Click> 事件引发时，会删除选定的行，除非它是新记录行（该行使用户可以添加新行）。  该行始终是 <xref:System.Windows.Forms.DataGridView> 控件中的最后一行。  
  
     当窗体的 <xref:System.Windows.Forms.Form.Load> 事件被引发时，会调用 `SetupLayout`、`SetupDataGridView` 和 `PopulateDataGridView` 实用工具方法。  
  
     当 <xref:System.Windows.Forms.DataGridView.CellFormatting> 事件被引发时，`Date` 列中的每个单元格都格式化为一个长日期，除非单元格的值无法分析。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#10)]  
  
## 测试应用程序  
 现在可以测试窗体，以确保其行为与预期相同。  
  
#### 测试窗体  
  
-   按 F5 运行该应用程序。  
  
     您将看到一个 <xref:System.Windows.Forms.DataGridView> 控件，它显示 `PopulateDataGridView` 中列出的歌曲。  可以使用**“添加行”**按钮添加新行，使用**“删除行”**按钮删除选定的行。  未绑定的 <xref:System.Windows.Forms.DataGridView> 控件是数据存储区，它的数据独立于任何外部源，如 <xref:System.Data.DataSet> 或数组。  
  
## 后续步骤  
 此应用程序使您对 <xref:System.Windows.Forms.DataGridView> 控件的功能有一个基本了解。  您可以通过以下几种方法来自定义 <xref:System.Windows.Forms.DataGridView> 控件的外观和行为：  
  
-   更改边框和标题样式。  有关更多信息，请参见 [如何：更改 Windows 窗体 DataGridView 控件中的边框和网格线的样式](../../../../docs/framework/winforms/controls/change-the-border-and-gridline-styles-in-the-datagrid.md)。  
  
-   允许或限制用户向 <xref:System.Windows.Forms.DataGridView> 控件中输入数据。  有关更多信息，请参见[如何：防止在 Windows 窗体 DataGridView 控件中添加和删除行](../../../../docs/framework/winforms/controls/prevent-row-addition-and-deletion-datagridview.md)和[如何：使 Windows 窗体 DataGridView 控件中的列只读](../../../../docs/framework/winforms/controls/how-to-make-columns-read-only-in-the-windows-forms-datagridview-control.md)。  
  
-   检查用户输入中是否有与数据库有关的错误。  有关更多信息，请参见 [演练：处理在 Windows 窗体 DataGridView 控件中输入数据时发生的错误](../../../../docs/framework/winforms/controls/handling-errors-that-occur-during-data-entry-in-the-datagrid.md)。  
  
-   使用虚拟模式处理特大数据集。  有关更多信息，请参见 [演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)。  
  
-   自定义单元格的外观。  有关更多信息，请参见 [如何：自定义 Windows 窗体 DataGridView 控件中单元格的外观](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md) 和 [如何：设置 Windows 窗体 DataGridView 控件的默认单元格样式](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 [在 Windows 窗体 DataGridView 控件中显示数据](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [如何：创建未绑定的 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/how-to-create-an-unbound-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的数据显示模式](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md)