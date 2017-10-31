---
title: "如何：更改 Windows 窗体 DataGridView 控件中的边框和网格线的样式 | Microsoft Docs"
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
  - "数据网格, 更改边框样式"
  - "数据网格, 更改网格线样式"
  - "DataGridView 控件 [Windows 窗体], 边框样式"
  - "DataGridView 控件 [Windows 窗体], 网格线样式"
  - "网格线, 更改样式"
ms.assetid: 2f413c7a-4025-4171-8e3a-66ef908ea583
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：更改 Windows 窗体 DataGridView 控件中的边框和网格线的样式
使用 <xref:System.Windows.Forms.DataGridView> 控件可以自定义控件边框和网格线的外观，以改善用户体验。  除可以修改控件内单元格的边框样式以外，还可以修改网格线颜色和控件边框样式。  还可以对普通单元格、行标题单元格和列标题单元格应用不同的单元格边框样式。  
  
> [!NOTE]
>  网格线颜色仅用于 <xref:System.Windows.Forms.DataGridViewCellBorderStyle> 枚举的 <xref:System.Windows.Forms.DataGridViewCellBorderStyle>、<xref:System.Windows.Forms.DataGridViewCellBorderStyle> 和 <xref:System.Windows.Forms.DataGridViewCellBorderStyle> 值，以及 <xref:System.Windows.Forms.DataGridViewHeaderBorderStyle> 枚举的 <xref:System.Windows.Forms.DataGridViewHeaderBorderStyle> 值。  这些枚举的其他值使用操作系统指定的颜色。  另外，在 Windows XP 和 Windows Server 2003 系列上通过 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName> 方法启用可视样式时，将不使用 <xref:System.Windows.Forms.DataGridView.GridColor%2A> 属性值。  
  
### 以编程方式更改网格线颜色  
  
-   设置 <xref:System.Windows.Forms.DataGridView.GridColor%2A> 属性。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#031](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#031)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#031](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#031)]  
  
### 以编程方式更改整个 DataGridView 控件的边框样式  
  
-   将 <xref:System.Windows.Forms.DataGridView.BorderStyle%2A> 属性设置为 <xref:System.Windows.Forms.BorderStyle> 枚举值之一。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#032](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#032)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#032](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#032)]  
  
### 以编程方式更改 DataGridView 单元格的边框样式  
  
-   设置 <xref:System.Windows.Forms.DataGridView.CellBorderStyle%2A>、<xref:System.Windows.Forms.DataGridView.RowHeadersBorderStyle%2A> 和 <xref:System.Windows.Forms.DataGridView.ColumnHeadersBorderStyle%2A> 属性。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#033](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#033)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#033](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#033)]  
  
## 示例  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#030](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#030)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#030](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#030)]  
  
## 编译代码  
 此示例需要：  
  
-   名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件。  
  
-   对 <xref:System?displayProperty=fullName>、<xref:System.Windows.Forms?displayProperty=fullName> 和 <xref:System.Drawing?displayProperty=fullName> 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.BorderStyle>   
 <xref:System.Windows.Forms.DataGridView.BorderStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.CellBorderStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.ColumnHeadersBorderStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.GridColor%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowHeadersBorderStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCellBorderStyle>   
 <xref:System.Windows.Forms.DataGridViewHeaderBorderStyle>   
 [Windows 窗体 DataGridView 控件中的基本格式设置和样式设置](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)