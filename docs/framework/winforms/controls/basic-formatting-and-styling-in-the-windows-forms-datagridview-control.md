---
title: "Windows 窗体 DataGridView 控件中的基本格式设置和样式设置 | Microsoft Docs"
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
  - "数据网格, 格式化"
  - "DataGridView 控件 [Windows 窗体], 格式设置和样式"
ms.assetid: b9b90836-1f56-4aa9-8db8-edc78fe830e8
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Windows 窗体 DataGridView 控件中的基本格式设置和样式设置
`DataGridView` 控件使您可以轻松定义单元格的基本外观和单元格值的显示格式。  可以通过设置 `DataGridViewCellStyle` 对象（可通过各种 `DataGridView` 控件属性访问它）的属性，来为单个单元格、为特定列和行中的单元格或者为控件中的所有单元格定义外观和格式样式。  另外，通过处理 `CellFormatting` 事件，可以基于诸如单元格值这样的因素来动态地修改这些样式。  
  
## 本节内容  
 [如何：更改 Windows 窗体 DataGridView 控件中的边框和网格线的样式](../../../../docs/framework/winforms/controls/change-the-border-and-gridline-styles-in-the-datagrid.md)  
 描述如何设置用于定义控件边框的外观和单元格之间的边界线的 `DataGridView` 属性。  
  
 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)  
 描述 `DataGridViewCellStyle` 类以及该类型的属性如何交互，以定义单元格在控件中的显示方式。  
  
 [如何：设置 Windows 窗体 DataGridView 控件的默认单元格样式](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)  
 描述如何使用 `DataGridViewCellStyle` 属性来定义在特定的行和列中以及在整个控件中的单元格的默认外观。  
  
 [如何：设置 Windows 窗体 DataGridView 控件中的数据格式](../../../../docs/framework/winforms/controls/how-to-format-data-in-the-windows-forms-datagridview-control.md)  
 描述如何使用 `DataGridViewCellStyle` 属性来格式化单元格的显示值。  
  
 [如何：设置 Windows 窗体 DataGridView 控件中的字体和颜色样式](../../../../docs/framework/winforms/controls/how-to-set-font-and-color-styles-in-the-windows-forms-datagridview-control.md)  
 描述如何使用 `DefaultCellStyle` 属性来为控件中的所有单元格设置基本显示特征。  
  
 [如何：为 Windows 窗体 DataGridView 控件设置交替行样式](../../../../docs/framework/winforms/controls/how-to-set-alternating-row-styles-for-the-windows-forms-datagridview-control.md)  
 描述如何使用以不同方式显示的交替行在控件中创建类似帐目型的效果。  
  
 [如何：使用行模板自定义 Windows 窗体 DataGridView 控件中的行](../../../../docs/framework/winforms/controls/use-the-row-template-to-customize-rows-in-the-datagrid.md)  
 描述如何使用 `RowTemplate` 属性来设置将用于控件中所有行的行属性。  
  
## 参考  
 <xref:System.Windows.Forms.DataGridView>  
 提供 <xref:System.Windows.Forms.DataGridView> 控件的参考文档。  
  
 <xref:System.Windows.Forms.DataGridViewCellStyle>  
 提供 <xref:System.Windows.Forms.DataGridViewCellStyle> 类的参考文档。  
  
 <xref:System.Windows.Forms.DataGridView.CellFormatting>  
 提供 <xref:System.Windows.Forms.DataGridView.CellFormatting> 事件的参考文档。  
  
 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A>  
 提供 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A> 属性的参考文档。  
  
## 相关章节  
 [自定义 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)  
 提供一些主题，描述了如何自定义绘制 <xref:System.Windows.Forms.DataGridView> 单元格和行，以及如何创建派生单元格、列和行类型。  
  
 [Windows 窗体 DataGridView 控件中的基本列、行和单元格功能](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)  
 提供描述常用的单元格、行和列属性的主题。  
  
## 请参阅  
 [DataGridView 控件](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)