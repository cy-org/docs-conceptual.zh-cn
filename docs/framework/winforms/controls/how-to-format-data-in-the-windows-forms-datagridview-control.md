---
title: "如何：设置 Windows 窗体 DataGridView 控件中的数据格式 | Microsoft Docs"
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
  - "单元格, 文本对齐"
  - "货币值, 数据网格中的格式设置"
  - "数据 [Windows 窗体], DataGridView 控件中的格式设置"
  - "数据网格, 货币值"
  - "数据网格, 日期值"
  - "数据网格, 启用换行"
  - "数据网格, 格式化数据"
  - "数据网格, 文本对齐"
  - "DataGridView 控件 [Windows 窗体], 格式化数据"
ms.assetid: 8c33543c-9c08-4636-a65a-fdf714a529b7
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：设置 Windows 窗体 DataGridView 控件中的数据格式
下面的过程演示如何使用 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A> 属性设置单元格值的基本格式，以及如何设置控件中特定列的基本格式。  有关数据的高级格式设置的信息，请参见[如何：自定义 Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)。  
  
### 设置货币和日期值的格式  
  
-   设置 <xref:System.Windows.Forms.DataGridViewCellStyle> 的 <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> 属性。  下面的代码示例使用列的 <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A> 属性设置特定列的格式。   `UnitPrice` 列中的值以特定于当前区域性的货币格式显示（负值用括号括起来）。   `ShipDate` 列中的值以特定于当前区域性的短日期格式显示。  有关 <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> 值的更多信息，请参见[格式化类型](../../../../docs/standard/base-types/formatting-types.md)。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#071](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#071)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#071](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#071)]  
  
### 自定义 null 数据库值的显示  
  
-   设置 <xref:System.Windows.Forms.DataGridViewCellStyle> 的 <xref:System.Windows.Forms.DataGridViewCellStyle.NullValue%2A> 属性。  下面的代码示例使用 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName> 属性在所有包含等于 <xref:System.DBNull.Value?displayProperty=fullName> 的值的单元格中显示“没有项”。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#073](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#073)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#073](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#073)]  
  
### 在基于文本的单元格中启用换行  
  
-   将 <xref:System.Windows.Forms.DataGridViewCellStyle> 的 <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewTriState> 枚举值之一。  下面的代码示例使用 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName> 属性设置整个控件的换行模式。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#074](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#074)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#074](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#074)]  
  
### 指定 DataGridView 单元格的文本对齐方式  
  
-   将 <xref:System.Windows.Forms.DataGridViewCellStyle> 的 <xref:System.Windows.Forms.DataGridViewCellStyle.Alignment%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewContentAlignment> 枚举值之一。  下面的代码示例使用列的 <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A> 属性设置特定列的对齐方式。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#072](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#072)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#072](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#072)]  
  
## 示例  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#070](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#070)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#070](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#070)]  
  
## 编译代码  
 这些示例要求：  
  
-   一个名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件，该控件包含名为 `UnitPrice` 的列、名为 `ShipDate` 的列和名为 `CustomerName` 的列。  
  
-   对 <xref:System?displayProperty=fullName>、<xref:System.Drawing?displayProperty=fullName> 和 <xref:System.Windows.Forms?displayProperty=fullName> 程序集的引用。  
  
## 可靠编程  
 为了获得最大可伸缩性，应该在使用相同样式的多个行、列或单元格中共享 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象，而不是单独设置每个元素的样式属性。  有关更多信息，请参见 [缩放 Windows 窗体 DataGridView 控件的最佳做法](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 [Windows 窗体 DataGridView 控件中的基本格式设置和样式设置](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/data-formatting-in-the-windows-forms-datagridview-control.md)   
 [如何：自定义 Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)   
 [格式化类型](../../../../docs/standard/base-types/formatting-types.md)