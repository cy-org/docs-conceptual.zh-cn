---
title: "自定义 Windows 窗体 DataGridView 控件 | Microsoft Docs"
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
  - "数据网格, 自定义"
  - "DataGridView 控件 [Windows 窗体], 自定义"
ms.assetid: 01ea5d4c-a736-4596-b0e9-a67a1b86e15f
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 自定义 Windows 窗体 DataGridView 控件
`DataGridView` 控件提供了多个可用来调整其单元格、行和列的外观和基本行为（外观和感受）的属性。  但是，如果您有超出 <xref:System.Windows.Forms.DataGridViewCellStyle> 类的功能之外的特殊需求，还可以实现控件的所有者描述，或者通过创建自定义单元格、列和行来扩展其功能。  
  
 若要自己绘制单元格和行，可以对各种 `DataGridView` 绘制事件进行处理。  若要修改现有功能或提供新的功能，可以创建自己的从现有的 `DataGridViewCell`、`DataGridViewColumn` 和 `DataGridViewRow` 类型派生的类型。  还可以通过创建派生类型来提供新的编辑功能，当单元格处于编辑模式时，该派生类型可以显示所选择的控件。  
  
## 本节内容  
 [如何：自定义 Windows 窗体 DataGridView 控件中单元格的外观](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md)  
 描述如何处理 <xref:System.Windows.Forms.DataGridView.CellPainting> 事件以手动绘制单元格。  
  
 [如何：自定义 Windows 窗体 DataGridView 控件中行的外观](../../../../docs/framework/winforms/controls/customize-the-appearance-of-rows-in-the-datagrid.md)  
 描述如何处理 <xref:System.Windows.Forms.DataGridView.RowPrePaint> 和 <xref:System.Windows.Forms.DataGridView.RowPostPaint> 事件以绘制具有自定义渐变背景和跨越多列的内容的行。  
  
 [如何：通过扩展 Windows 窗体 DataGridView 控件中单元格和列的行为和外观对其进行自定义](../../../../docs/framework/winforms/controls/customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md)  
 描述如何创建从 `DataGridViewCell` 和 `DataGridViewColumn` 派生的自定义类型，以便在将鼠标指针停留在单元格上方时突出显示该单元格。  
  
 [如何：禁用 Windows 窗体 DataGridView 控件的按钮列中的按钮](../../../../docs/framework/winforms/controls/disable-buttons-in-a-button-column-in-the-datagrid.md)  
 描述如何创建从 <xref:System.Windows.Forms.DataGridViewButtonCell> 和 <xref:System.Windows.Forms.DataGridViewButtonColumn> 派生的自定义类型，以便在按钮列中显示禁用的按钮。  
  
 [如何：在 Windows 窗体 DataGridView 单元格中承载控件](../../../../docs/framework/winforms/controls/how-to-host-controls-in-windows-forms-datagridview-cells.md)  
 描述如何实现 `IDataGridViewEditingControl` 接口以及如何创建从 `DataGridViewCell` 和 `DataGridViewColumn` 派生的自定义类型，以便当单元格处于编辑模式时显示 <xref:System.Windows.Forms.DateTimePicker> 控件。  
  
## 参考  
 <xref:System.Windows.Forms.DataGridView>  
 提供 <xref:System.Windows.Forms.DataGridView> 控件的参考文档。  
  
 <xref:System.Windows.Forms.DataGridViewCell>  
 提供 <xref:System.Windows.Forms.DataGridViewCell> 类的参考文档。  
  
 <xref:System.Windows.Forms.DataGridViewRow>  
 提供 <xref:System.Windows.Forms.DataGridViewRow> 类的参考文档。  
  
 <xref:System.Windows.Forms.DataGridViewColumn>  
 提供 <xref:System.Windows.Forms.DataGridViewColumn> 类的参考文档。  
  
 <xref:System.Windows.Forms.IDataGridViewEditingControl>  
 提供 <xref:System.Windows.Forms.IDataGridViewEditingControl> 接口的参考文档。  
  
## 相关章节  
 [Windows 窗体 DataGridView 控件中的基本格式设置和样式设置](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)  
 提供一些主题，描述了如何修改控件的基本外观和单元格数据的显示格式。  
  
## 请参阅  
 [DataGridView 控件](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)   
 [Windows 窗体 DataGridView 控件中的列类型](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)