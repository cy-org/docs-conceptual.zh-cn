---
title: "如何：冻结 Windows 窗体 DataGridView 控件中的列 | Microsoft Docs"
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
  - "列 [Windows 窗体], 冻结"
  - "DataGridView 控件 [Windows 窗体], 列始终在视图中"
  - "DataGridView 控件 [Windows 窗体], 冻结列"
ms.assetid: 2ef8b1de-782e-4867-af8d-58171ab5c106
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：冻结 Windows 窗体 DataGridView 控件中的列
用户查看 Windows 窗体 <xref:System.Windows.Forms.DataGridView> 控件中显示的数据时，有时需要频繁地引用单个列或列集。  例如，显示包含许多列的客户信息表时，使其他列可在可使区域外滚动的同时始终显示客户姓名非常有用。  
  
 若要实现此行为，可冻结控件中的列。  冻结列时，也将冻结其左侧（在从右到左的语言脚本中为右侧）的所有列。  冻结的列保持不变，而所有其他列可以滚动。  
  
> [!NOTE]
>  如果启用了列重新排序，冻结的列被视为一组不同于未冻结的列。  用户可重新定位任一组中的列，但不能将列从一个组移到另一组。  
  
 列的 <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A> 属性决定列在网格内是否始终可见。  
  
 Visual Studio 中对此任务提供支持。  另请参阅[如何：使用设计器冻结 Windows 窗体 DataGridView 控件中的列](http://msdn.microsoft.com/library/kaswfbes%20\(v=vs.717\))。  
  
### 以编程方式冻结列  
  
-   将 <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A?displayProperty=fullName> 属性设置为 `true`。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#061](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#061)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#061](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#061)]  
  
## 编译代码  
 此示例需要：  
  
-   名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件，其包含一个名为 `AddToCartButton` 的列。  
  
-   对 <xref:System?displayProperty=fullName> 和 <xref:System.Windows.Forms?displayProperty=fullName> 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView>   
 [Windows 窗体 DataGridView 控件中的基本列、行和单元格功能](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)   
 [如何：启用 Windows 窗体 DataGridView 控件中列的重新排序](../../../../docs/framework/winforms/controls/how-to-enable-column-reordering-in-the-windows-forms-datagridview-control.md)