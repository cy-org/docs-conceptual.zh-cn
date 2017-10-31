---
title: "DataGridView 控件体系结构（Windows 窗体） | Microsoft Docs"
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
  - "DataGridView 控件 [Windows 窗体], 体系结构"
ms.assetid: 1c6cabf0-02ee-4bbc-9574-b54bb7f5b19e
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# DataGridView 控件体系结构（Windows 窗体）
<xref:System.Windows.Forms.DataGridView> 控件及其相关类旨在提供一个灵活的可扩展系统，用于显示和编辑表格数据。  这些类全部包含在 <xref:System.Windows.Forms?displayProperty=fullName> 命名空间中，并全部以“DataGridView”前缀命名。  
  
## 结构元素  
 主要的 <xref:System.Windows.Forms.DataGridView> 伴生类从 <xref:System.Windows.Forms.DataGridViewElement> 派生。  下面的对象模型演示了 <xref:System.Windows.Forms.DataGridViewElement> 继承层次结构。  
  
 ![DataGridViewElement 对象模型](../../../../docs/framework/winforms/controls/media/datagridviewelement.png "DataGridViewElement")  
DataGridViewElement 对象模型  
  
 <xref:System.Windows.Forms.DataGridViewElement> 类提供对 <xref:System.Windows.Forms.DataGridView> 父控件的引用，并具有一个 <xref:System.Windows.Forms.DataGridViewElement.State%2A> 属性，该属性所包含的值由 <xref:System.Windows.Forms.DataGridViewElementStates> 枚举的值组合而成。  
  
 以下各节对 <xref:System.Windows.Forms.DataGridView> 伴生类进行了更详细地介绍。  
  
### DataGridViewElementStates  
 <xref:System.Windows.Forms.DataGridViewElementStates> 枚举包含下列值：  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
 可以使用按位逻辑运算符对此枚举的值进行组合，因此 <xref:System.Windows.Forms.DataGridViewElement.State%2A> 属性一次可以表示多个状态。  例如，<xref:System.Windows.Forms.DataGridViewElement> 可以同时表示 <xref:System.Windows.Forms.DataGridViewElementStates>、<xref:System.Windows.Forms.DataGridViewElementStates> 和 <xref:System.Windows.Forms.DataGridViewElementStates>。  
  
### 单元格和带区  
 <xref:System.Windows.Forms.DataGridView> 控件由两种基本类型的对象组成：单元格和带区。  所有单元格都是从 <xref:System.Windows.Forms.DataGridViewCell> 基类派生的。  两种类型的带区（<xref:System.Windows.Forms.DataGridViewColumn> 和 <xref:System.Windows.Forms.DataGridViewRow>）都是从 <xref:System.Windows.Forms.DataGridViewBand> 基类派生的。  
  
 <xref:System.Windows.Forms.DataGridView> 控件可以与多个类进行互操作，但最常用的类为 <xref:System.Windows.Forms.DataGridViewCell>、<xref:System.Windows.Forms.DataGridViewColumn> 和 <xref:System.Windows.Forms.DataGridViewRow>。  
  
### DataGridViewCell  
 单元格是 <xref:System.Windows.Forms.DataGridView> 的基本交互单元。  单元格中的内容居中显示，并且通常通过单元格来输入数据。  通过使用 <xref:System.Windows.Forms.DataGridViewRow> 类的 <xref:System.Windows.Forms.DataGridViewRow.Cells%2A> 集合可以访问单元格，通过使用 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> 集合可以访问选定的单元格。  下面的对象模型演示了此用法，并显示 <xref:System.Windows.Forms.DataGridViewCell> 继承层次结构。  
  
 ![DataGridViewCell 对象模型](../../../../docs/framework/winforms/controls/media/datagridviewcell.png "DataGridViewCell")  
DataGridViewCell 对象模型  
  
 <xref:System.Windows.Forms.DataGridViewCell> 类型是一个抽象基类，所有单元格类型都是从该类派生的。  <xref:System.Windows.Forms.DataGridViewCell> 及其派生类型不是 Windows 窗体控件，但有些类型可以承载 Windows 窗体控件。  单元格所支持的任何编辑功能通常都由被承载的控件进行处理。  
  
 <xref:System.Windows.Forms.DataGridViewCell> 对象不能像 Windows 窗体控件那样控制自己的外观和绘制功能，  而是由 <xref:System.Windows.Forms.DataGridView> 负责其 <xref:System.Windows.Forms.DataGridViewCell> 对象的外观。  通过与 <xref:System.Windows.Forms.DataGridView> 控件的属性和事件进行交互操作，可以显著影响单元格的外观和行为。  如果您有超出 <xref:System.Windows.Forms.DataGridView> 控件的功能之外的特殊自定义需求，可以实现自己的从 <xref:System.Windows.Forms.DataGridViewCell> 或其某个子类派生的类。  
  
 下表显示从 <xref:System.Windows.Forms.DataGridViewCell> 派生的类：  
  
-   <xref:System.Windows.Forms.DataGridViewTextBoxCell>  
  
-   <xref:System.Windows.Forms.DataGridViewButtonCell>  
  
-   <xref:System.Windows.Forms.DataGridViewLinkCell>  
  
-   <xref:System.Windows.Forms.DataGridViewCheckBoxCell>  
  
-   <xref:System.Windows.Forms.DataGridViewComboBoxCell>  
  
-   <xref:System.Windows.Forms.DataGridViewImageCell>  
  
-   <xref:System.Windows.Forms.DataGridViewHeaderCell>  
  
-   <xref:System.Windows.Forms.DataGridViewRowHeaderCell>  
  
-   <xref:System.Windows.Forms.DataGridViewColumnHeaderCell>  
  
-   <xref:System.Windows.Forms.DataGridViewTopLeftHeaderCell>  
  
-   自定义单元格类型  
  
### DataGridViewColumn  
 <xref:System.Windows.Forms.DataGridView> 控件的附加数据存储区的架构通过 <xref:System.Windows.Forms.DataGridView> 控件的列来表示。  可以使用 <xref:System.Windows.Forms.DataGridView.Columns%2A> 集合访问 <xref:System.Windows.Forms.DataGridView> 控件的列。  可以使用 <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> 集合访问选定的列。  下面的对象模型演示了此用法，并显示 <xref:System.Windows.Forms.DataGridViewColumn> 继承层次结构。  
  
 ![DataGridViewColumn 对象模型](../../../../docs/framework/winforms/controls/media/datagridviewcolumn.png "DataGridViewColumn")  
DataGridViewColumn 对象模型  
  
 一些主要的单元格类型具有相应的列类型。  这些列类型是从 <xref:System.Windows.Forms.DataGridViewColumn> 基类派生的。  
  
 下表显示从 <xref:System.Windows.Forms.DataGridViewColumn> 派生的类：  
  
-   <xref:System.Windows.Forms.DataGridViewButtonColumn>  
  
-   <xref:System.Windows.Forms.DataGridViewCheckBoxColumn>  
  
-   <xref:System.Windows.Forms.DataGridViewComboBoxColumn>  
  
-   <xref:System.Windows.Forms.DataGridViewImageColumn>  
  
-   <xref:System.Windows.Forms.DataGridViewTextBoxColumn>  
  
-   <xref:System.Windows.Forms.DataGridViewLinkColumn>  
  
-   自定义列类型  
  
### DataGridView 编辑控件  
 支持高级编辑功能的单元格通常使用从 Windows 窗体控件派生的寄宿的控件。  这些控件还实现 <xref:System.Windows.Forms.IDataGridViewEditingControl> 接口。  下面的对象模型演示了这些控件的用法。  
  
 ![DataGridView 编辑控件对象模型](../../../../docs/framework/winforms/controls/media/datagridviewediting.png "DataGridViewEditing")  
DataGridView 编辑控件对象模型  
  
 随 <xref:System.Windows.Forms.DataGridView> 控件一起提供了下列编辑控件：  
  
-   <xref:System.Windows.Forms.DataGridViewComboBoxEditingControl>  
  
-   <xref:System.Windows.Forms.DataGridViewTextBoxEditingControl>  
  
 有关创建自己的编辑控件的信息，请参见[如何：在 Windows 窗体 DataGridView 单元格中承载控件](../../../../docs/framework/winforms/controls/how-to-host-controls-in-windows-forms-datagridview-cells.md)。  
  
 下表阐释了单元格类型、列类型和编辑控件之间的关系。  
  
|单元格类型|寄宿的控件|列类型|  
|-----------|-----------|---------|  
|<xref:System.Windows.Forms.DataGridViewButtonCell>|无|<xref:System.Windows.Forms.DataGridViewButtonColumn>|  
|<xref:System.Windows.Forms.DataGridViewCheckBoxCell>|无|<xref:System.Windows.Forms.DataGridViewCheckBoxColumn>|  
|<xref:System.Windows.Forms.DataGridViewComboBoxCell>|<xref:System.Windows.Forms.DataGridViewComboBoxEditingControl>|<xref:System.Windows.Forms.DataGridViewComboBoxColumn>|  
|<xref:System.Windows.Forms.DataGridViewImageCell>|无|<xref:System.Windows.Forms.DataGridViewImageColumn>|  
|<xref:System.Windows.Forms.DataGridViewLinkCell>|无|<xref:System.Windows.Forms.DataGridViewLinkColumn>|  
|<xref:System.Windows.Forms.DataGridViewTextBoxCell>|<xref:System.Windows.Forms.DataGridViewTextBoxEditingControl>|<xref:System.Windows.Forms.DataGridViewTextBoxColumn>|  
  
### DataGridViewRow  
 <xref:System.Windows.Forms.DataGridViewRow> 类显示 <xref:System.Windows.Forms.DataGridView> 控件附加到的数据存储区中的某记录的数据字段。  通过使用 <xref:System.Windows.Forms.DataGridView.Rows%2A> 集合可以访问 <xref:System.Windows.Forms.DataGridView> 控件的行。  通过使用 <xref:System.Windows.Forms.DataGridView.SelectedRows%2A> 集合可以访问选定的行。  下面的对象模型演示了此用法，并显示 <xref:System.Windows.Forms.DataGridViewRow> 继承层次结构。  
  
 ![DataGridViewRow 对象模型](../../../../docs/framework/winforms/controls/media/datagridviewrow.png "DataGridViewRow")  
DataGridViewRow 对象模型  
  
 您可以从 <xref:System.Windows.Forms.DataGridViewRow> 类派生自己的类型，尽管通常无需这么做。  <xref:System.Windows.Forms.DataGridView> 控件具有一些与行相关的事件和属性，可以用于自定义其 <xref:System.Windows.Forms.DataGridViewRow> 对象的行为。  
  
 如果启用 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> 属性，则将会在最后一行显示一个用于添加新行的特殊行。  此行是 <xref:System.Windows.Forms.DataGridView.Rows%2A> 集合的一部分，但您可能需要关注其所具有的特殊功能。  有关更多信息，请参见[在 Windows 窗体 DataGridView 控件中使用新记录行](../../../../docs/framework/winforms/controls/using-the-row-for-new-records-in-the-windows-forms-datagridview-control.md)。  
  
## 请参阅  
 [DataGridView 控件概述](../../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md)   
 [自定义 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)   
 [在 Windows 窗体 DataGridView 控件中使用新记录行](../../../../docs/framework/winforms/controls/using-the-row-for-new-records-in-the-windows-forms-datagridview-control.md)