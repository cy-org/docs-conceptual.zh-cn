---
title: "如何：设置 Windows 窗体 DataGridView 控件中列的排序模式 | Microsoft Docs"
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
  - "数据网格, 对数据进行排序"
  - "DataGridView 控件 [Windows 窗体], 排序模式"
  - "排序, 数据网格"
ms.assetid: 57dfed60-a608-40d5-86f9-d65686ffb325
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：设置 Windows 窗体 DataGridView 控件中列的排序模式
在 <xref:System.Windows.Forms.DataGridView> 控件中，默认情况下文本框列使用自动排序，而其他列类型不自动排序。  有时您会希望重写这些默认设置。  例如，可以显示图像来替换文本、数字或枚举单元格值。  虽然无法排序图像，但可以排序它们表示的基础值。  
  
 在 <xref:System.Windows.Forms.DataGridView> 控件中，列的 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 属性值确定其排序行为。  
  
 下面的过程显示来自 [如何：自定义 Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md) 的 `Priority` 列。  此列为图像列，默认情况下是不可排序的。  但是它包含的实际单元格值为字符串，因此它可以被自动排序。  
  
### 设置列的排序模式  
  
-   设置 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=fullName> 属性。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#066](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#066)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#066](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#066)]  
  
## 编译代码  
 此示例需要：  
  
-   一个名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件，其中包含一个名为 `Priority` 的列。  
  
-   对 <xref:System?displayProperty=fullName> 和 <xref:System.Windows.Forms?displayProperty=fullName> 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=fullName>   
 [对 Windows 窗体 DataGridView 控件中的数据排序](../../../../docs/framework/winforms/controls/sorting-data-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的列排序模式](../../../../docs/framework/winforms/controls/column-sort-modes-in-the-windows-forms-datagridview-control.md)   
 [如何：自定义 Windows 窗体 DataGridView 控件中的排序方式](../../../../docs/framework/winforms/controls/how-to-customize-sorting-in-the-windows-forms-datagridview-control.md)