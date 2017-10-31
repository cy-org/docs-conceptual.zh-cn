---
title: "DataGridView 控件概述（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "DataGridView"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "绑定控件, DataGridView 控件"
  - "列 [Windows 窗体], DataGridView 控件"
  - "数据 [Windows 窗体], 导航"
  - "数据 [Windows 窗体], 重新排序"
  - "Data Binding — 数据绑定, DataGridView 控件"
  - "数据网格, 关于数据网格"
  - "数据源, 绑定到 DataGridView 控件"
  - "DataGridView 控件 [Windows 窗体], 关于 DataGridView 控件"
  - "DataGridView 控件 [Windows 窗体], Data Binding — 数据绑定"
  - "数据集 [Windows 窗体], 绑定到 DataGridView 控件"
  - "网格控件 [Windows 窗体]"
  - "网格 [Windows 窗体]"
  - "表 [Windows 窗体], 绑定到 DataGridView 控件"
  - "表 [Windows 窗体], 在 DataGridView 控件中显示"
ms.assetid: 0a45c661-89dc-4390-9cc6-c47eee501488
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# DataGridView 控件概述（Windows 窗体）
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 使用 <xref:System.Windows.Forms.DataGridView> 控件，可以显示和编辑来自多种不同类型的数据源的表格数据。  
  
 将数据绑定到 <xref:System.Windows.Forms.DataGridView> 控件非常简单和直观，在大多数情况下，只需设置 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 属性即可。  在绑定到包含多个列表或表的数据源时，只需将 <xref:System.Windows.Forms.DataGridView.DataMember%2A> 属性设置为指定要绑定的列表或表的字符串即可。  
  
 <xref:System.Windows.Forms.DataGridView> 控件支持标准 Windows 窗体数据绑定模型，因此该控件将绑定到下表所述的类的实例：  
  
-   任何实现 <xref:System.Collections.IList> 接口的类，包括一维数组。  
  
-   任何实现 <xref:System.ComponentModel.IListSource> 接口的类，例如 <xref:System.Data.DataTable> 和 <xref:System.Data.DataSet> 类。  
  
-   任何实现 <xref:System.ComponentModel.IBindingList> 接口的类，例如 <xref:System.ComponentModel.BindingList%601> 类。  
  
-   任何实现 <xref:System.ComponentModel.IBindingListView> 接口的类，例如 <xref:System.Windows.Forms.BindingSource> 类。  
  
 <xref:System.Windows.Forms.DataGridView> 控件支持对这些接口所返回对象的公共属性的数据绑定，如果在返回的对象上实现 <xref:System.ComponentModel.ICustomTypeDescriptor> 接口，则还支持对该接口所返回的属性集合的数据绑定。  
  
 通常绑定到 <xref:System.Windows.Forms.BindingSource> 组件，并将 <xref:System.Windows.Forms.BindingSource> 组件绑定到其他数据源或使用业务对象填充该组件。  <xref:System.Windows.Forms.BindingSource> 组件为首选数据源，因为该组件可以绑定到各种数据源，并可以自动解决许多数据绑定问题。  有关更多信息，请参见 [BindingSource 组件](../../../../docs/framework/winforms/controls/bindingsource-component.md)。  
  
 <xref:System.Windows.Forms.DataGridView> 控件还可以在“取消绑定”模式下使用，无需任何基础数据存储区。  有关使用未绑定的 <xref:System.Windows.Forms.DataGridView> 控件的代码示例，请参见 [演练：创建未绑定的 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/walkthrough-creating-an-unbound-windows-forms-datagridview-control.md)。  
  
 <xref:System.Windows.Forms.DataGridView> 控件具有极高的可配置性和可扩展性，它提供有大量的属性、方法和事件，可以用来对该控件的外观和行为进行自定义。  当需要在 Windows 窗体应用程序中显示表格数据时，请首先考虑使用 <xref:System.Windows.Forms.DataGridView> 控件，然后再考虑使用其他控件（例如 <xref:System.Windows.Forms.DataGrid>）。  若要以小型网格显示只读值，或者若要使用户能够编辑具有数百万条记录的表，<xref:System.Windows.Forms.DataGridView> 控件将为您提供可以方便地进行编程以及有效地利用内存的解决方案。  
  
## 本节内容  
 [DataGridView 控件技术摘要](../../../../docs/framework/winforms/controls/datagridview-control-technology-summary-windows-forms.md)  
 概括介绍 <xref:System.Windows.Forms.DataGridView> 控件的概念和相关类的用法。  
  
 [DataGridView 控件体系结构](../../../../docs/framework/winforms/controls/datagridview-control-architecture-windows-forms.md)  
 描述 <xref:System.Windows.Forms.DataGridView> 的结构，解释其类型层次结构和继承结构。  
  
 [DataGridView 控件应用方案](../../../../docs/framework/winforms/controls/datagridview-control-scenarios-windows-forms.md)  
 描述使用 <xref:System.Windows.Forms.DataGridView> 控件的最常见方案。  
  
 [DataGridView 控件代码目录](../../../../docs/framework/winforms/controls/datagridview-control-code-directory-windows-forms.md)  
 提供指向文档中各种 <xref:System.Windows.Forms.DataGridView> 任务的代码示例的链接。  这些示例按任务类型进行分类。  
  
## 相关章节  
 [Windows 窗体 DataGridView 控件中的列类型](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)  
 讨论 Windows 窗体 <xref:System.Windows.Forms.DataGridView> 控件中用于显示信息以及允许用户修改或添加信息的列类型。  
  
 [在 Windows 窗体 DataGridView 控件中显示数据](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)  
 提供描述如何使用数据手动填充控件或通过外部数据源填充控件的主题。  
  
 [自定义 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)  
 提供一些主题，描述了如何自定义绘制 <xref:System.Windows.Forms.DataGridView> 单元格和行，以及如何创建派生单元格、列和行类型。  
  
 [Windows 窗体 DataGridView 控件中的性能优化](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)  
 提供一些主题，描述了如何有效地使用该控件，以避免在处理大量数据时出现性能问题。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 [DataGridView 控件](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)   
 [Windows 窗体 DataGridView 控件中的默认功能](../../../../docs/framework/winforms/controls/default-functionality-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的默认键盘和鼠标处理](../../../../docs/framework/winforms/controls/default-keyboard-and-mouse-handling-in-the-windows-forms-datagridview-control.md)