---
title: "DataGridView 控件方案（Windows 窗体） | Microsoft Docs"
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
  - "数据网格, 关于数据网格"
  - "DataGridView 控件 [Windows 窗体], 方案"
ms.assetid: 09a5fd05-3447-47ec-a4ec-6082a2b7f0dd
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# DataGridView 控件方案（Windows 窗体）
使用 <xref:System.Windows.Forms.DataGridView> 控件，可以从各种数据源显示表格数据。  对于简单的使用场合，可以手动填充 <xref:System.Windows.Forms.DataGridView>，直接通过该控件操作数据。  但是，通常将数据存储在外部数据源中，并通过 <xref:System.Windows.Forms.BindingSource> 组件将此控件绑定到该数据源。  
  
 本主题描述调用 <xref:System.Windows.Forms.DataGridView> 控件的一些常用方案。  
  
## 方案 1：显示少量数据  
 不必将数据存储到外部数据源即可在 <xref:System.Windows.Forms.DataGridView> 控件中显示该数据。  若要处理少量数据，可以自己手动填充该控件，通过控件来操作数据。  这称为“取消绑定模式”。  有关更多信息，请参见 [如何：创建未绑定的 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/how-to-create-an-unbound-windows-forms-datagridview-control.md)。  
  
### 方案关键点  
  
-   在取消绑定模式下，您需要手动填充该控件。  
  
-   取消绑定模式特别适用于少量只读数据。  
  
-   取消绑定模式还适用于类似于电子表格的表或稀疏填充的表。  
  
## 方案 2：查看和更新外部数据源中存储的数据  
 可以使用 <xref:System.Windows.Forms.DataGridView> 控件作为用户界面 \(UI\)，用户可以通过该界面访问数据源（例如数据库表或业务对象集合）中保存的数据。  有关更多信息，请参见 [如何：将数据绑定到 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/how-to-bind-data-to-the-windows-forms-datagridview-control.md)。  
  
### 方案关键点  
  
-   使用绑定模式可以连接到数据源，基于数据源属性或数据库列自动生成列，并自动填充该控件。  
  
-   绑定模式适用于需要对数据执行大量用户交互的场合。  可以设置数据的显示格式，可以将用户指定的数据解析为数据源所需的格式。  可以检测数据输入格式错误和数据库约束错误，以便向用户发出警告，并更正错误的单元格。  
  
-   其他功能（例如列排序、冻结和重新排序）使用户能够以最适合于其工作流的方式来查看数据。  
  
-   剪贴板支持使用户能够将数据从应用程序复制到其他应用程序。  
  
## 方案 3：高级数据  
 如果您有标准数据绑定模型无法满足的特殊需求，可以通过实现“虚拟模式”来管理该控件与数据之间的交互。  实现虚拟模式是指实现一个或多个事件处理程序，将针对单元格的控件请求信息限定为所需的信息。  
  
 例如，若要处理大量的数据，则可能需要实现虚拟模式以确保最佳的效率。  在维护与从其他数据源检索数据的列一同显示的未绑定列的值方面，虚拟模式非常有用。  
  
 有关虚拟模式的更多信息，请参见 [演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)。  
  
### 方案关键点  
  
-   虚拟模式适用于在需要优化性能的场合显示数量非常巨大的数据。  
  
## 方案 4：自动调整行和列的大小  
 在显示需要定期更新的数据时，可以自动调整行和列的大小以确保可以看到所有内容。  <xref:System.Windows.Forms.DataGridView> 控件提供了多个选项，使您能够启用或禁用手动调整大小、在特定时间以编程方式调整大小或在内容更改时自动调整大小。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件中的大小调整选项](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md)。  
  
### 方案关键点  
  
-   手动调整大小允许用户调整单元格的高度和宽度。  
  
-   自动调整大小允许您维护单元格的大小，以便永远不用剪裁单元格的内容。  
  
-   以编程方式调整大小允许您在特定的时间调整单元格的大小，以避免连续调整大小对性能的影响。  
  
## 方案 5：简单自定义  
 <xref:System.Windows.Forms.DataGridView> 控件提供了多种用于修改该控件的基本外观和行为的方法。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)。  
  
### 方案关键点  
  
-   通过 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象，您可以在多个级别上为该控件的各个元素提供颜色、字体、格式设置和定位信息。  
  
-   单元格样式可以进行分层并由多个元素共享，从而允许重用代码。  
  
## 方案 6：高级自定义  
 <xref:System.Windows.Forms.DataGridView> 控件提供了多种用于自定义该控件的外观和行为的方法。  
  
### 方案关键点  
  
-   您可以提供自己的单元格绘制代码。  有关更多信息，请参见 [如何：自定义 Windows 窗体 DataGridView 控件中单元格的外观](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md)。  
  
-   您可以提供自己的行绘制方式。  这一功能非常有用，例如创建内容跨越多个列的行时。  有关更多信息，请参见 [如何：自定义 Windows 窗体 DataGridView 控件中行的外观](../../../../docs/framework/winforms/controls/customize-the-appearance-of-rows-in-the-datagrid.md)。  
  
-   您可以实现自己的单元格类和列类以自定义单元格的外观。  有关更多信息，请参见 [如何：通过扩展 Windows 窗体 DataGridView 控件中单元格和列的行为和外观对其进行自定义](../../../../docs/framework/winforms/controls/customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md)。  
  
-   您可以实现自己的单元格类和列类（不使用内置的列类型所提供的类）来承载控件。  有关更多信息，请参见 [如何：在 Windows 窗体 DataGridView 单元格中承载控件](../../../../docs/framework/winforms/controls/how-to-host-controls-in-windows-forms-datagridview-cells.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 [DataGridView 控件概述](../../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md)