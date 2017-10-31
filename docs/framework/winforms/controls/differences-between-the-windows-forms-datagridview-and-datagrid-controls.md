---
title: "Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别 | Microsoft Docs"
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
  - "数据网格"
  - "DataGrid 控件 [Windows 窗体], 进行比较的 DataGridView 控件"
  - "DataGridView 控件 [Windows 窗体], 进行比较的 DataGrid 控件"
ms.assetid: d412c786-140e-4210-8a56-a68467530a55
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别
<xref:System.Windows.Forms.DataGridView> 控件是替换 <xref:System.Windows.Forms.DataGrid> 控件的新控件。  <xref:System.Windows.Forms.DataGridView> 控件提供了 <xref:System.Windows.Forms.DataGrid> 控件中没有的许多基本功能和高级功能。  此外，<xref:System.Windows.Forms.DataGridView> 控件的结构使得它比 <xref:System.Windows.Forms.DataGrid> 控件更容易扩展和自定义。  
  
 下表描述 <xref:System.Windows.Forms.DataGridView> 控件中提供而 <xref:System.Windows.Forms.DataGrid> 控件中未提供的几个主要功能。  
  
|DataGridView 控件功能|说明|  
|-----------------------|--------|  
|多种列类型|与 <xref:System.Windows.Forms.DataGrid> 控件相比，<xref:System.Windows.Forms.DataGridView> 控件提供了更多的内置列类型。  这些列类型能满足大多数常见方案的需要，而且比 <xref:System.Windows.Forms.DataGrid> 控件中的列类型更容易扩展或替换。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件中的列类型](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)。|  
|多种数据显示方式|<xref:System.Windows.Forms.DataGrid> 控件仅限于显示外部数据源的数据。  而 <xref:System.Windows.Forms.DataGridView> 控件可显示存储在控件中的未绑定数据、来自绑定数据源的数据或者同时显示绑定数据和未绑定数据。  也可以在 <xref:System.Windows.Forms.DataGridView> 控件中实现虚拟模式以提供自定义数据管理。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件中的数据显示模式](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md)。|  
|用于自定义数据显示的多种方式|<xref:System.Windows.Forms.DataGridView> 控件提供了许多属性和事件，您可以使用它们指定数据的格式设置方式和显示方式。  例如，您可以根据单元格、行和列中包含的数据更改其外观，或者将一种数据类型的数据替换为另一种类型的等效数据。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/data-formatting-in-the-windows-forms-datagridview-control.md)。|  
|用于更改单元格、行、列、标头外观和行为的多个选项|<xref:System.Windows.Forms.DataGridView> 控件使您能够以多种方式使用各个网格组件。  例如，您可以冻结行和列以阻止其滚动；隐藏行、列和标头；更改调整行、列和标头大小的方式；更改用户进行选择的方式；以及为各个单元格、行和列提供工具提示和快捷菜单。|  
  
 保留了 <xref:System.Windows.Forms.DataGrid> 控件，以备向后兼容和特殊需要。  但几乎所有目的都应使用 <xref:System.Windows.Forms.DataGridView> 控件来实现。  <xref:System.Windows.Forms.DataGrid> 控件中提供而 <xref:System.Windows.Forms.DataGridView> 控件中未提供的唯一功能是在一个控件中分层显示两个相关表中的信息。  您必须使用两个 <xref:System.Windows.Forms.DataGridView> 控件显示具有主\/详细信息关系的两个表中的信息。  
  
## 升级为 DataGridView 控件  
 如果现有应用程序在简单数据绑定方案中使用未进行自定义的 <xref:System.Windows.Forms.DataGrid> 控件，则可以简单地使用新控件替换旧控件。  这两种控件均使用标准的 Windows 窗体数据绑定结构，因此 <xref:System.Windows.Forms.DataGridView> 控件无需使用附加配置即可显示绑定数据。  您可能会想要利用改进的数据绑定功能，实际上，您可将数据绑定到 <xref:System.Windows.Forms.BindingSource> 组件，然后将该组件绑定到 <xref:System.Windows.Forms.DataGridView> 控件。  有关更多信息，请参见 [BindingSource 组件](../../../../docs/framework/winforms/controls/bindingsource-component.md)。  
  
 因为 <xref:System.Windows.Forms.DataGridView> 控件具有全新的结构，所以不存在可将 <xref:System.Windows.Forms.DataGrid> 自定义用于 <xref:System.Windows.Forms.DataGridView> 控件的直接转换路径。  但是，由于新控件提供了内置功能，许多 <xref:System.Windows.Forms.DataGrid> 自定义对 <xref:System.Windows.Forms.DataGridView> 控件来说是不必要的。  如果您已为 <xref:System.Windows.Forms.DataGrid> 控件创建了自定义列类型并想要将这些类型用于 <xref:System.Windows.Forms.DataGridView> 控件，则必须使用新结构重新实现它们。  有关更多信息，请参见 [自定义 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGrid>   
 <xref:System.Windows.Forms.BindingSource>   
 [DataGridView 控件](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)   
 [DataGrid 控件](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [BindingSource 组件](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [Windows 窗体 DataGridView 控件中的列类型](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的数据显示模式](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/data-formatting-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的大小调整选项](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的列排序模式](../../../../docs/framework/winforms/controls/column-sort-modes-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的选择模式](../../../../docs/framework/winforms/controls/selection-modes-in-the-windows-forms-datagridview-control.md)   
 [自定义 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)