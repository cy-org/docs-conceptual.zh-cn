---
title: "Windows 窗体 DataGridView 控件的选项和剪贴板使用 | Microsoft Docs"
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
  - "单元格, 在网格中选择"
  - "剪贴板, 在 DataGridView 控件中"
  - "数据网格, 选择单元格"
  - "DataGridView 控件 [Windows 窗体], 使用剪贴板"
  - "DataGridView 控件 [Windows 窗体], 选择单元格"
  - "选择, 在 DataGridView 控件中"
ms.assetid: 82cffcad-8b30-4897-bddb-c3a79d751b83
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Windows 窗体 DataGridView 控件的选项和剪贴板使用
`DataGridView` 控件提供各种选项，用于配置用户选择单元格、行和列的方式。  例如，您可以启用一个或多个选项，在用户单击单元格时选择整行或整列，或者仅当用户单击行标题或列标题时选择整行或整列（同时也选择了单元格）。  如果您想要为选项提供自己的用户界面，可以禁用普通选项并用编程方式处理所有选项。  另外，可以允许用户将所选值复制到剪贴板。  
  
## 本节内容  
 [Windows 窗体 DataGridView 控件中的选择模式](../../../../docs/framework/winforms/controls/selection-modes-in-the-windows-forms-datagridview-control.md)  
 描述为用户以及控件中的编程选择提供的选项。  
  
 [如何：设置 Windows 窗体 DataGridView 控件的选择模式](../../../../docs/framework/winforms/controls/how-to-set-the-selection-mode-of-the-windows-forms-datagridview-control.md)  
 描述如何配置控件，以便当用户单击单元格时选择单行。  
  
 [如何：获取 Windows 窗体 DataGridView 控件中选定的单元格、行和列](../../../../docs/framework/winforms/controls/selected-cells-rows-and-columns-datagridview.md)  
 描述如何处理所选单元格、行和列集合。  
  
 [如何：使用户能够将多个单元格从 Windows 窗体 DataGridView 控件复制到剪贴板](../../../../docs/framework/winforms/controls/enable-users-to-copy-multiple-cells-to-the-clipboard-datagridview.md)  
 描述如何在控件中启用剪贴板支持。  
  
## 参考  
 <xref:System.Windows.Forms.DataGridView>  
 提供 <xref:System.Windows.Forms.DataGridView> 控件的参考文档。  
  
 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=fullName>  
 提供 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 属性的参考文档。  
  
 <xref:System.Windows.Forms.DataGridView.ClipboardCopyMode%2A>  
 提供 <xref:System.Windows.Forms.DataGridView.ClipboardCopyMode%2A> 属性的参考文档。  
  
 <xref:System.Windows.Forms.DataGridViewSelectedCellCollection>  
 提供 <xref:System.Windows.Forms.DataGridViewSelectedCellCollection> 类的参考文档。  
  
 <xref:System.Windows.Forms.DataGridViewSelectedRowCollection>  
 提供 <xref:System.Windows.Forms.DataGridViewSelectedRowCollection> 类的参考文档。  
  
 <xref:System.Windows.Forms.DataGridViewSelectedColumnCollection>  
 提供 <xref:System.Windows.Forms.DataGridViewSelectedColumnCollection> 类的参考文档。  
  
## 请参阅  
 [DataGridView 控件](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)   
 [Windows 窗体 DataGridView 控件中的默认键盘和鼠标处理](../../../../docs/framework/winforms/controls/default-keyboard-and-mouse-handling-in-the-windows-forms-datagridview-control.md)