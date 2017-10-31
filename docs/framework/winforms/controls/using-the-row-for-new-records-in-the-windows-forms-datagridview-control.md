---
title: "在 Windows 窗体 DataGridView 控件中使用新记录行 | Microsoft Docs"
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
  - "DataGridView 控件 [Windows 窗体], 为新记录添加行"
  - "DataGridView 控件 [Windows 窗体], 数据输入"
  - "行, 新建记录"
ms.assetid: 6110f1ea-9794-442c-a98a-f104a1feeaf4
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 在 Windows 窗体 DataGridView 控件中使用新记录行
在应用程序中使用 <xref:System.Windows.Forms.DataGridView> 编辑数据时，经常希望使用户能够向数据存储区添加新的数据行。  <xref:System.Windows.Forms.DataGridView> 控件通过为新记录提供一行（总是显示为最后一行）来支持此功能。  该行在其行标头中用星号 \(\*\) 标记。  以下各节讨论在启用新记录行后编程时应考虑的一些问题。  
  
## 显示新记录行  
 使用 <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> 属性可指示是否显示新记录行。  此属性的默认值为 `true`。  
  
 对于数据绑定的情况，如果控件的 <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> 属性和数据源的 <xref:System.ComponentModel.IBindingList.AllowNew%2A?displayProperty=fullName> 属性均为 `true`，则将显示新记录行。  如果其中的一个属性为 `false`，则不显示该行。  
  
## 用默认数据填充新记录行  
 当用户选择新记录行作为当前行时，<xref:System.Windows.Forms.DataGridView> 控件引发 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded> 事件。  
  
 此事件提供对新 <xref:System.Windows.Forms.DataGridViewRow> 的访问，并使您能够用默认数据填充该新行。  有关更多信息，请参见 [如何：为 Windows 窗体 DataGridView 控件中的新行指定默认值](../../../../docs/framework/winforms/controls/specify-default-values-for-new-rows-in-the-datagrid.md)  
  
## 行集合  
 新记录行包含在 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.Rows%2A> 集合中，但在两个方面具有不同的行为：  
  
-   不能以编程方式将新记录行从 <xref:System.Windows.Forms.DataGridView.Rows%2A> 集合中移除。  如果尝试执行此操作，将引发 <xref:System.InvalidOperationException>。  用户也不能删除新记录行。  <xref:System.Windows.Forms.DataGridViewRowCollection.Clear%2A?displayProperty=fullName> 方法不会从 <xref:System.Windows.Forms.DataGridView.Rows%2A> 集合中移除此行。  
  
-   不能在新记录行之后添加任何行。  如果尝试执行此操作，将引发 <xref:System.InvalidOperationException>。  因此，新记录行总是 <xref:System.Windows.Forms.DataGridView> 控件中的最后一行。  存在新记录行时，<xref:System.Windows.Forms.DataGridViewRowCollection> 中添加行的方法（<xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A>、<xref:System.Windows.Forms.DataGridViewRowCollection.AddCopy%2A> 和 <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopies%2A>）都在内部调用插入方法。  
  
## 新记录行的视觉自定义  
 创建新记录行时，新记录行基于由 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A> 属性指定的行。  没有为此行指定的任何单元格样式都将从其他属性继承。  有关单元格样式继承的更多信息，请参见 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)。  
  
 新记录行中的单元格显示的初始值是从每个单元格的 <xref:System.Windows.Forms.DataGridViewCell.DefaultNewRowValue%2A> 属性检索得到的。  对于类型为 <xref:System.Windows.Forms.DataGridViewImageCell> 的单元格，此属性返回一个占位符图像。  对于其他类型的单元格，此属性返回 `null`。  可以重写此属性以返回自定义值。  但是，当焦点进入新记录行时，这些初始值可以被 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded> 事件处理程序替换。  
  
 用于此行标头的标准图标（箭头或星号）不是公开的。  如果要自定义这些图标，需要创建一个自定义的 <xref:System.Windows.Forms.DataGridViewRowHeaderCell> 类。  
  
 标准图标使用行标头单元格所使用的 <xref:System.Windows.Forms.DataGridViewCellStyle> 的 <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> 属性。  如果没有完整显示所需的足够空间，就不呈现这些标准图标。  
  
 如果行标头单元格已设置了字符串值，并且没有足够的空间既显示文本又显示图标，则首先放弃图标。  
  
## 排序  
 在取消绑定模式中，即使用户已对 <xref:System.Windows.Forms.DataGridView> 的内容排序，也总是将新记录添加到 <xref:System.Windows.Forms.DataGridView> 的末尾。  用户将需要重新应用该排序以便将该行排列到正确的位置；此行为类似于 <xref:System.Windows.Forms.ListView> 控件的行为。  
  
 在数据绑定和虚拟模式中，应用了排序以后的插入行为将取决于数据模型的实现。  对于 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)]，将立刻将该行排列到正确的位置。  
  
## 关于新记录行的其他说明  
 不能将此行的 <xref:System.Windows.Forms.DataGridViewRow.Visible%2A> 属性设置为 `false`。  如果尝试执行此操作，将引发 <xref:System.InvalidOperationException>。  
  
 新记录行总是在未选中状态下创建。  
  
## 虚拟模式  
 如果要实现虚拟模式，您需要对以下情况进行跟踪：在数据模型中何时需要新记录行；何时回滚该行的添加操作。  此功能的正确实现取决于数据模型的实现及其事务语义，例如，提交范围是在单元格级还是在行级。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件中的虚拟模式](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded?displayProperty=fullName>   
 [Windows 窗体 DataGridView 控件中的数据输入](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)   
 [如何：为 Windows 窗体 DataGridView 控件中的新行指定默认值](../../../../docs/framework/winforms/controls/specify-default-values-for-new-rows-in-the-datagrid.md)