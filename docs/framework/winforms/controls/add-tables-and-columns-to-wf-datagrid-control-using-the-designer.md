---
title: "如何：使用设计器向 Windows 窗体 DataGrid 控件添加表和列 | Microsoft Docs"
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
  - "列 [Windows 窗体], 添加到 DataGrid 控件"
  - "DataGrid 控件 [Windows 窗体], 添加表和列"
  - "表 [Windows 窗体], 添加到 DataGrid 控件"
ms.assetid: 4a6d1b34-b696-476b-bf8a-57c6230aa9e1
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用设计器向 Windows 窗体 DataGrid 控件添加表和列
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 通过创建 <xref:System.Windows.Forms.DataGridTableStyle> 对象并将它们添加到 <xref:System.Windows.Forms.GridTableStylesCollection> 对象（此对象通过 <xref:System.Windows.Forms.DataGrid> 控件的 <xref:System.Windows.Forms.DataGrid.TableStyles%2A> 属性访问）中，可以在 Windows 窗体 <xref:System.Windows.Forms.DataGrid> 控件中以表和列的形式显示数据。  每个表样式显示在 <xref:System.Windows.Forms.DataGridTableStyle> 的 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> 属性中指定的任意数据表的内容。  默认情况下，未指定列样式的表样式将显示该数据表中的所有列。  通过将 <xref:System.Windows.Forms.DataGridColumnStyle> 对象添加到 <xref:System.Windows.Forms.GridColumnStylesCollection>（可以通过每个 <xref:System.Windows.Forms.DataGridTableStyle> 的 <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 属性访问）中，可以限制显示表中的哪些列。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，该项目拥有一个包含 <xref:System.Windows.Forms.DataGrid> 控件的窗体。  有关如何设置此类项目的信息，请参见 [How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa) 和 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  在 [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)] 中，默认情况下，<xref:System.Windows.Forms.DataGrid> 控件不在**“工具箱”**中。  有关添加该控件的信息，请参见[How to: Add Items to the Toolbox](http://msdn.microsoft.com/zh-cn/458e119e-17fe-450b-b889-e31c128bd7e0)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计器中向 DataGrid 控件添加表  
  
1.  为在表中显示数据，必须首先将 <xref:System.Windows.Forms.DataGrid> 控件绑定到数据集。  有关更多信息，请参见 [如何：使用设计器将 Windows 窗体 DataGrid 控件绑定到数据源](../../../../docs/framework/winforms/controls/bind-wf-datagrid-control-to-a-data-source-using-the-designer.md)。  
  
2.  在“属性”窗口中选择 <xref:System.Windows.Forms.DataGrid> 控件的 <xref:System.Windows.Forms.DataGrid.TableStyles%2A> 属性，然后单击该属性旁边的省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)，以显示**“DataGridTableStyle 集合编辑器”**。  
  
3.  在集合编辑器中，单击**“添加”**以插入表样式。  
  
4.  单击**“确定”**关闭集合编辑器，然后单击 <xref:System.Windows.Forms.DataGrid.TableStyles%2A> 属性旁边的省略号按钮将其重新打开。  
  
     在重新打开集合编辑器后，绑定到该控件的所有数据表都会显示在该表样式的 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> 属性的下拉列表中。  
  
5.  在集合编辑器的**“成员”**框中，单击该表样式。  
  
6.  在集合编辑器的**“属性”**框中，选择要显示的表的 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> 值。  
  
### 在设计器中向 DataGrid 控件添加列  
  
1.  在**“DataGridTableStyle 集合编辑器”**的**“成员”**框中，选择适当的表样式。  在集合编辑器的**“属性”**框中，选择 <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 集合，然后单击该属性旁边的省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) 以显示**“DataGridColumnStyle 集合编辑器”**。  
  
2.  在集合编辑器中，单击**“添加”**以插入列样式或单击**“添加”**旁边的向下箭头以指定列类型。  
  
     在下拉框中，可以选择 <xref:System.Windows.Forms.DataGridTextBoxColumn> 或 <xref:System.Windows.Forms.DataGridBoolColumn> 类型。  
  
3.  单击“确定”以关闭**“DataGridColumnStyle 集合编辑器”**，然后单击 <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 属性旁边的省略号按钮将其重新打开。  
  
     在重新打开集合编辑器后，绑定数据表中的所有数据列都会显示在该列样式的 <xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A> 属性的下拉列表中。  
  
4.  在集合编辑器的**“成员”**框中，单击该列样式。  
  
5.  在集合编辑器的**“属性”**框中，选择要显示的列的 <xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A> 值。  
  
## 请参阅  
 [DataGrid 控件](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [如何：在 Windows 窗体 DataGrid 控件中删除或隐藏列](../../../../docs/framework/winforms/controls/how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)