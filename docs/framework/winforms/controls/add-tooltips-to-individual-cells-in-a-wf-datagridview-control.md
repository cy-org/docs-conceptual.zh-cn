---
title: "如何：为 Windows 窗体 DataGridView 控件中的单个单元格添加工具提示 | Microsoft Docs"
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
  - "数据网格, 添加工具提示"
  - "DataGridView 控件 [Windows 窗体], 添加工具提示"
  - "工具提示 [Windows 窗体], 添加到数据网格"
ms.assetid: 2a81f9de-d58b-4ea8-bc0b-8d93c2f4cf78
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：为 Windows 窗体 DataGridView 控件中的单个单元格添加工具提示
默认情况下，工具提示用于显示因为单元格太小而无法显示其完整内容的 <xref:System.Windows.Forms.DataGridView> 单元格的值。  但您可以重写此行为，以便为各单元格设置工具提示文本值。  这在向用户显示有关单元格的附加信息或为用户提供有关单元格内容的替代说明时很有用。  例如，如果有一行显示状态图标，您可能希望使用工具提示提供文本说明。  
  
 还可以通过将 <xref:System.Windows.Forms.DataGridView.ShowCellToolTips%2A?displayProperty=fullName> 属性设置为 `false` 来禁止显示单元格级的工具提示。  
  
### 向单元格添加工具提示  
  
-   设置 <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A?displayProperty=fullName> 属性。  
  
     [!code-cpp[System.Windows.Forms.DataGridViewCell.ToolTipText#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCell.ToolTipText/cpp/datagridviewcell.tooltiptext.cpp#1)]
     [!code-csharp[System.Windows.Forms.DataGridViewCell.ToolTipText#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCell.ToolTipText/CS/datagridviewcell.tooltiptext.cs#1)]
     [!code-vb[System.Windows.Forms.DataGridViewCell.ToolTipText#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCell.ToolTipText/VB/datagridviewcell.tooltiptext.vb#1)]  
  
## 编译代码  
  
-   此示例需要：  
  
-   一个名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件，其中包含一个名为 `Rating` 列，该列用于显示一至四个星号 \("\*"\) 的字符串值。  控件的 <xref:System.Windows.Forms.DataGridView.CellFormatting> 事件必须与示例中所示的事件处理程序方法关联。  
  
-   对 <xref:System?displayProperty=fullName> 和 <xref:System.Windows.Forms?displayProperty=fullName> 程序集的引用。  
  
## 可靠编程  
 将 <xref:System.Windows.Forms.DataGridView> 控件绑定到外部数据源或通过实现虚拟模式提供自己的数据源时，可能会遇到性能问题。  为避免在处理大量数据时损失性能，请处理 <xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded> 事件而不是设置多个单元格的 <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A> 属性。  处理此事件时，获取单元格的 <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A> 属性的值会引发该事件并按事件处理程序中的指定返回 <xref:System.Windows.Forms.DataGridViewCellToolTipTextNeededEventArgs.ToolTipText%2A?displayProperty=fullName> 属性的值。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.ShowCellToolTips%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCell>   
 <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A?displayProperty=fullName>   
 [使用 Windows 窗体 DataGridView 控件中的单元格、行和列编程](../../../../docs/framework/winforms/controls/programming-with-cells-rows-and-columns-in-the-datagrid.md)