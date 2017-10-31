---
title: "DataGridView 控件（Windows 窗体） | Microsoft Docs"
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
  - "数据 [Windows 窗体], 以表格形式显示"
  - "数据网格"
  - "数据表示"
  - "DataGridView 控件 [Windows 窗体]"
  - "数据集 [Windows 窗体], 在 DataGridView 控件中显示"
  - "数据集 [Windows 窗体], 用户界面"
  - "网格控件 [Windows 窗体]"
  - "表 [Windows 窗体]"
  - "表格数据, 在 Windows 窗体上显示"
  - "Windows 窗体, 显示数据"
ms.assetid: dbee73f2-bba6-4874-9389-cd21d44309be
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# DataGridView 控件（Windows 窗体）
`DataGridView` 控件提供一种以表格格式显示数据的功能强大且灵活的方法。  可以使用 `DataGridView` 控件来显示少量数据的只读视图，或者可以缩放该控件以显示大型数据集的可编辑视图。  
  
 可以使用多种方法扩展 `DataGridView` 控件，以便将自定义行为置入你的应用程序中。  例如，可以以编程方式指定自己的排序算法，并且可以创建自己的单元格类型。  可以通过在多个属性之间进行选择来轻松地自定义 `DataGridView` 控件的外观。  许多数据存储类型均可用作数据源，或者，`DataGridView` 控件可以在不绑定任何数据源的情况下进行操作。  
  
 本节中的主题介绍可用于将 `DataGridView` 功能构建到应用程序中的概念和技术。  
  
## 本节内容  
 [DataGridView 控件概述](../../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md)  
 提供一些主题，介绍 Windows 窗体 `DataGridView` 控件的体系结构和核心概念。  
  
 [Windows 窗体 DataGridView 控件中的默认功能](../../../../docs/framework/winforms/controls/default-functionality-in-the-windows-forms-datagridview-control.md)  
 描述 Windows 窗体 `DataGridView` 控件在绑定到数据源时的默认外观和行为。  
  
 [Windows 窗体 DataGridView 控件中的列类型](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)  
 描述 Windows 窗体 `DataGridView` 控件中用于显示数据和允许用户修改或添加数据的列类型。  
  
 [Windows 窗体 DataGridView 控件中的基本列、行和单元格功能](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)  
 提供一些主题，描述常用的单元格、行和列属性。  
  
 [Windows 窗体 DataGridView 控件中的基本格式设置和样式设置](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)  
 提供一些主题，描述如何修改该控件的基本外观和单元数据的显示格式。  
  
 [在 Windows 窗体 DataGridView 控件中显示数据](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)  
 提供一些主题，描述如何手动或从外部数据源向控件填充数据。  
  
 [调整 Windows 窗体 DataGridView 控件中列和行的大小](../../../../docs/framework/winforms/controls/resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)  
 提供一些主题，描述可如何自动调整行和列的大小，以便适应单元格内容，或适应该控件的可用宽度。  
  
 [对 Windows 窗体 DataGridView 控件中的数据排序](../../../../docs/framework/winforms/controls/sorting-data-in-the-windows-forms-datagridview-control.md)  
 提供介绍控件中的排序功能的主题。  
  
 [Windows 窗体 DataGridView 控件中的数据输入](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)  
 提供一些主题，介绍如何改变用户添加和修改控件中数据的方式。  
  
 [Windows 窗体 DataGridView 控件的选项和剪贴板使用](../../../../docs/framework/winforms/controls/selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)  
 提供一些主题，介绍控件中的单元格、行和列选择功能。  
  
 [使用 Windows 窗体 DataGridView 控件中的单元格、行和列编程](../../../../docs/framework/winforms/controls/programming-with-cells-rows-and-columns-in-the-datagrid.md)  
 提供一些主题，介绍如何使用单元格、行和列对象进行编程。  
  
 [自定义 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)  
 提供一些主题，介绍自定义绘制 `DataGridView` 单元格和行，以及创建派生的单元、列和行类型。  
  
 [Windows 窗体 DataGridView 控件中的性能优化](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)  
 提供一些主题，介绍如何在使用大量数据时，有效地使用控件以避免性能问题。  
  
 [Windows 窗体 DataGridView 控件中的默认键盘和鼠标处理](../../../../docs/framework/winforms/controls/default-keyboard-and-mouse-handling-in-the-windows-forms-datagridview-control.md)  
 介绍用户可如何通过键盘和鼠标与 `DataGridView` 控件进行交互。  
  
 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)  
 描述 `DataGridView` 控件如何改进和替换 <xref:System.Windows.Forms.DataGrid> 控件。  
  
 另请参阅[将设计器与 Windows 窗体 DataGridView 控件结合使用](http://msdn.microsoft.com/library/171593w110ac%20\(v=vs.110\))。  
  
## 参考  
 <xref:System.Windows.Forms.DataGridView>  
 提供关于 <xref:System.Windows.Forms.DataGridView> 控件的参考文档。  
  
 <xref:System.Windows.Forms.BindingSource>  
 提供关于 <xref:System.Windows.Forms.BindingSource> 组件的参考文档。  <xref:System.Windows.Forms.DataGridView> 控件和 <xref:System.Windows.Forms.BindingSource> 组件设计为需紧密协作。  
  
## 请参阅  
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)