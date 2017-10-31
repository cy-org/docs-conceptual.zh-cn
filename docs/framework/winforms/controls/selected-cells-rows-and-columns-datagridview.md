---
title: "如何：获取 Windows 窗体 DataGridView 控件中选定的单元格、行和列 | Microsoft Docs"
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
  - "DataGridView 控件 [Windows 窗体], 获取选定内容"
  - "获取选定内容, DataGridView 控件 [Windows 窗体]"
  - "选择, DataGridView 控件 [Windows 窗体]"
ms.assetid: d93c4b5b-498e-49bc-982a-2229d61778e4
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：获取 Windows 窗体 DataGridView 控件中选定的单元格、行和列
您可以使用 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A>、<xref:System.Windows.Forms.DataGridView.SelectedRows%2A> 和 <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> 属性相应地从 <xref:System.Windows.Forms.DataGridView> 控件中获取选中的单元格、行或列。  在下面的过程中，您将获取选中的单元格，并将其行索引和列索引显示在 <xref:System.Windows.Forms.MessageBox> 中。  
  
### 获取 DataGridView 控件中选中的单元格  
  
-   使用 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> 属性。  
  
    > [!NOTE]
    >  使用 <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A> 方法可避免显示可能具有大量数据的单元格。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#10)]  
  
### 获取 DataGridView 控件中选中的行  
  
-   使用 <xref:System.Windows.Forms.DataGridView.SelectedRows%2A> 属性。  若要使用户能够选择行，您必须将 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode>。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#20)]  
  
### 获取 DataGridView 控件中选中的列  
  
-   使用 <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> 属性。  若要使用户能够选择列，您必须将 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewSelectionMode> 或 <xref:System.Windows.Forms.DataGridViewSelectionMode>。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#30)]  
  
## 编译代码  
 此示例需要：  
  
-   名为 `selectedCellsButton`、`selectedRowsButton` 和 `selectedColumnsButton` 的 <xref:System.Windows.Forms.Button> 控件，每个控件均应附加有 <xref:System.Windows.Forms.Control.Click> 事件处理程序。  
  
-   名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件。  
  
-   对 <xref:System?displayProperty=fullName>、<xref:System.Windows.Forms?displayProperty=fullName> 和 <xref:System.Text?displayProperty=fullName> 程序集的引用。  
  
## 可靠编程  
 此主题中描述的集合在选择了大量单元格、行或列时不能有效执行。  有关使用这些具有大量数据的集合的更多信息，请参见 [缩放 Windows 窗体 DataGridView 控件的最佳做法](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A>   
 <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A>   
 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A>   
 <xref:System.Windows.Forms.DataGridView.SelectedRows%2A>   
 <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A>   
 [Windows 窗体 DataGridView 控件的选项和剪贴板使用](../../../../docs/framework/winforms/controls/selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)