---
title: "DataGridView 控件技术摘要（Windows 窗体） | Microsoft Docs"
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
  - "数据网格, 关于数据网格"
  - "DataGridView 控件 [Windows 窗体], 关于 DataGridView 控件"
ms.assetid: 094498c3-a126-4a3f-83fe-f69e96c7717b
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# DataGridView 控件技术摘要（Windows 窗体）
本主题概括介绍 `DataGridView` 控件以及支持使用该控件的类的相关信息。  
  
 以表格格式显示数据是一项可能需要频繁执行的任务。  `DataGridView` 控件是专门用于以网格形式显示数据的完整解决方案。  
  
## 关键字  
 DataGridView、BindingSource、表、单元格、数据绑定、虚拟模式  
  
## 命名空间  
 <xref:System.Windows.Forms?displayProperty=fullName>  
  
 <xref:System.Data?displayProperty=fullName>  
  
## 相关技术  
 `BindingSource`  
  
## 背景  
 用户界面 \(UI\) 设计人员经常会发现需要向用户显示表格数据。  [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 提供了多种以表或网格形式显示数据的方式。  `DataGridView` 控件代表着此技术在 Windows 窗体应用程序中的最新进展。  
  
 `DataGridView` 控件可以显示数据存储区中的数据行。  支持多种类型的数据存储区。  数据存储区可以保存简单的非类型化数据（例如一维数组），也可以保存类型化数据（例如 <xref:System.Data.DataSet>）。  有关更多信息，请参见 [如何：将数据绑定到 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/how-to-bind-data-to-the-windows-forms-datagridview-control.md)。  
  
 `DataGridView` 控件提供一种以表格格式显示数据的强大且灵活的方式。  您可以使用该控件显示小型到大型数据集的只读或可编辑视图。  
  
 可以采用多种方法对 `DataGridView` 控件进行扩展，以将自定义行为内置在应用程序中。  例如，可以采用编程方式指定自己的排序算法，以及创建自己的单元格类型。  通过选择一些属性，可以轻松地自定义 `DataGridView` 控件的外观。  可以将许多类型的数据存储区用作数据源，也可以在没有绑定数据源的情况下操作 `DataGridView` 控件。  
  
## 实现 DataGridView 类  
 可以通过多种方法利用 `DataGridView` 控件的扩展性功能。  通过事件和属性可以对该控件的许多方面进行自定义，但是一些自定义需要创建从现有的 `DataGridView` 类派生的新类。  
  
 最常用的基类为 `DataGridViewCell` 和 `DataGridViewColumn`。  可以从 `DataGridViewCell` 或其任意子类派生自己的单元格类。  尽管可以向任何列添加任意单元格类型，但您通常还是会从 `DataGridViewColumn` 派生一个伴生列类，用于在默认情况下承载自定义单元格类型的单元格。  
  
 您可以在派生的单元格类中实现 `IDataGridViewEditingCell` 接口，以创建具有编辑功能但不能在编辑模式下承载控件的单元格类型。  若要创建可在编辑模式下在单元格中承载的控件，可以在从 <xref:System.Windows.Forms.Control> 派生的类中实现 `IDataGridViewEditingControl` 接口。  
  
 有关更多信息，请参见 [如何：通过扩展 Windows 窗体 DataGridView 控件中单元格和列的行为和外观对其进行自定义](../../../../docs/framework/winforms/controls/customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md) 和 [如何：在 Windows 窗体 DataGridView 单元格中承载控件](../../../../docs/framework/winforms/controls/how-to-host-controls-in-windows-forms-datagridview-cells.md)。  
  
## DataGridView 类概览  
 <xref:System.Windows.Forms>  
  
|技术领域|类\/接口\/配置元素|  
|----------|-----------------|  
|数据绑定|<xref:System.Windows.Forms.BindingSource>|  
|数据表示|<xref:System.Windows.Forms.DataGridView><br /><br /> <xref:System.Windows.Forms.DataGridViewCell> 和派生类<br /><br /> <xref:System.Windows.Forms.DataGridViewRow> 和派生类<br /><br /> <xref:System.Windows.Forms.DataGridViewColumn> 和派生类<br /><br /> <xref:System.Windows.Forms.DataGridViewCellStyle>|  
|<xref:System.Windows.Forms.DataGridView> 扩展性|<xref:System.Windows.Forms.DataGridViewCell> 和派生类<br /><br /> <xref:System.Windows.Forms.DataGridViewColumn> 和派生类<br /><br /> <xref:System.Windows.Forms.IDataGridViewEditingCell><br /><br /> <xref:System.Windows.Forms.IDataGridViewEditingControl>|  
  
## 新增功能  
 <xref:System.Windows.Forms.DataGridView> 控件是专门用于在 Windows 窗体中显示表格数据的完整解决方案。  在创作新的应用程序时，应首先考虑使用 <xref:System.Windows.Forms.DataGridView> 控件，然后再考虑采用其他解决方案（例如 <xref:System.Windows.Forms.DataGrid>）。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 <xref:System.Windows.Forms.DataGridView> 控件可以与 <xref:System.Windows.Forms.BindingSource> 组件紧密地结合使用。  此组件旨在用作窗体的主要数据源。  无论数据源采用何种类型，它都可以管理 <xref:System.Windows.Forms.DataGridView> 控件与其数据源之间的交互。  
  
## 请参阅  
 [DataGridView 控件概述](../../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md)   
 [DataGridView 控件体系结构](../../../../docs/framework/winforms/controls/datagridview-control-architecture-windows-forms.md)   
 [保护连接信息](../../../../docs/framework/data/adonet/protecting-connection-information.md)