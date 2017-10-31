---
title: "如何：自定义 Windows 窗体 DataGridView 控件中单元格的外观 | Microsoft Docs"
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
  - "单元格, 在 DataGridView 控件中自定义"
  - "数据网格, 自定义单元格"
  - "DataGridView 控件 [Windows 窗体], 自定义单元格"
ms.assetid: 478b20c9-625c-4116-9c5c-5a16e6f4ec67
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：自定义 Windows 窗体 DataGridView 控件中单元格的外观
可以通过处理 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.CellPainting> 事件自定义任一单元格的外观。  可以从 <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs> 的 <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs.Graphics%2A> 属性中提取 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Drawing.Graphics>。  使用此 <xref:System.Drawing.Graphics> 可以影响整个 <xref:System.Windows.Forms.DataGridView> 控件的外观，但是您通常希望仅影响当前正在绘制的单元格的外观。  <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs> 的 <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs.ClipBounds%2A> 属性使您能够将绘制操作限制于当前正在绘制的单元格上。  
  
 在下面的代码示例中，将使用 <xref:System.Windows.Forms.DataGridView> 控件的配色方案绘制 `ContactName` 列中的所有单元格。  每个单元格的文本内容均以 <xref:System.Drawing.Color.Crimson%2A> 绘制，并且以与 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.GridColor%2A> 属性相同的颜色绘制一个内嵌的矩形。  
  
## 示例  
 [!code-csharp[System.Windows.Forms.DataGridViewCellPainting#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCellPainting/CS/form1.cs#10)]
 [!code-vb[System.Windows.Forms.DataGridViewCellPainting#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCellPainting/VB/form1.vb#10)]  
  
## 编译代码  
 此示例需要：  
  
-   一个名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件，该控件包含一个 `ContactName` 列（如同 Northwind 示例数据库的 Customers 表中的同名列）。  
  
-   对 System、System.Windows.Forms 和 System.Drawing 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.CellPainting>   
 [自定义 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)