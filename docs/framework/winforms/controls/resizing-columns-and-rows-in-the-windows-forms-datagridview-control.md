---
title: "调整 Windows 窗体 DataGridView 控件中列和行的大小 | Microsoft Docs"
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
  - "列 [Windows 窗体], 在网格中调整大小"
  - "数据网格, 调整列和行的大小"
  - "DataGridView 控件 [Windows 窗体], 调整行和列的大小"
ms.assetid: 7532764d-e5c1-4943-a08b-6377a722d3b6
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 调整 Windows 窗体 DataGridView 控件中列和行的大小
`DataGridView` 控件为自定义列和行的调整大小行为提供了大量选项。  通常，`DataGridView` 单元格不基于自身内容来调整大小，  而是剪辑任何大于该单元格的显示值。  如果内容可以作为字符串显示，则单元格在 ToolTip 中显示该内容。  
  
 默认情况下，用户可以用鼠标拖动行、列和标题分隔符来显示更多信息。  也可以双击分隔符以基于内容自动调整关联的行、列或标题带区。  
  
 `DataGridView` 控件提供属性、方法和事件，使您可以自定义或禁用所有这些用户定向行为。  另外，您可以用编程方式调整行、列和标题的大小来适应其内容，或者将它们配置为每当内容更改时自动调整其自身大小。  也可以对列进行配置，以便按照您指定的比例划分控件的可用宽度。  
  
## 本节内容  
 [Windows 窗体 DataGridView 控件中的大小调整选项](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md)  
 描述用于调整行、列和标题大小的选项。  还提供了与调整大小相关的属性和方法的详细信息，并描述了常用方案。  
  
 [Windows 窗体 DataGridView 控件中的列填充模式](../../../../docs/framework/winforms/controls/column-fill-mode-in-the-windows-forms-datagridview-control.md)  
 详细描述列填充模式，并提供了可以用来体验列填充模式和其他模式的演示代码。  
  
 [如何：设置 Windows 窗体 DataGridView 控件的大小调整模式](../../../../docs/framework/winforms/controls/how-to-set-the-sizing-modes-of-the-windows-forms-datagridview-control.md)  
 描述如何为常见用途配置调整大小模式。  
  
 [如何：以编程方式调整单元格的大小来适应 Windows 窗体 DataGridView 控件中的内容](../../../../docs/framework/winforms/controls/programmatically-resize-cells-to-fit-content-in-the-datagrid.md)  
 提供可以用来体验以编程方式调整大小的演示代码。  
  
 [如何：自动调整单元格的大小来适应 Windows 窗体 DataGridView 控件中的内容变化](../../../../docs/framework/winforms/controls/automatically-resize-cells-when-content-changes-in-the-datagrid.md)  
 提供可以用来体验自动调整大小模式的演示代码。  
  
## 参考  
 <xref:System.Windows.Forms.DataGridView>  
 提供 <xref:System.Windows.Forms.DataGridView> 控件的参考文档。  
  
## 请参阅  
 [DataGridView 控件](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)