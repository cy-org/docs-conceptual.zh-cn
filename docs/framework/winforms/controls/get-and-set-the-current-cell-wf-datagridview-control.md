---
title: "如何：获取和设置 Windows 窗体 DataGridView 控件中的当前单元格 | Microsoft Docs"
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
  - "单元格, 获取和设置当前单元格"
  - "DataGridView 控件 [Windows 窗体], 获取当前单元格"
  - "DataGridView 控件 [Windows 窗体], 设置当前单元格"
ms.assetid: b0e41e57-493a-4bd0-9376-a6f76723540c
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：获取和设置 Windows 窗体 DataGridView 控件中的当前单元格
若要与 <xref:System.Windows.Forms.DataGridView> 进行交互，通常要求通过编程方式发现哪个单元格当前处于活动状态。  您可能还需要更改当前单元格。  可通过 <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> 属性执行这些任务。  
  
> [!NOTE]
>  您不能在 <xref:System.Windows.Forms.DataGridViewBand.Visible%2A> 属性设置为 `false` 的行或列中设置当前单元格。  
  
 根据 <xref:System.Windows.Forms.DataGridView> 控件的选择模式的不同，更改当前单元格可能会更改选择。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件中的选择模式](../../../../docs/framework/winforms/controls/selection-modes-in-the-windows-forms-datagridview-control.md)。  
  
### 通过编程方式获取当前单元格  
  
-   使用 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> 属性。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#080](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#080)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#080](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#080)]  
  
### 通过编程方式设置当前单元格  
  
-   设置 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> 属性。  在下面的代码示例中，当前单元格设置为 0 行 1 列。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#085](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#085)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#085](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#085)]  
  
## 编译代码  
 此示例需要：  
  
-   名为 `getCurrentCellButton` 和 `setCurrentCellButton` 的 <xref:System.Windows.Forms.Button> 控件。  在 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 中，您必须将每个按钮的 <xref:System.Windows.Forms.Control.Click> 事件附加到该代码示例中的关联事件处理程序。  
  
-   名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件。  
  
-   对 <xref:System?displayProperty=fullName> 和 <xref:System.Windows.Forms?displayProperty=fullName> 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.CurrentCell%2A?displayProperty=fullName>   
 [Windows 窗体 DataGridView 控件中的基本列、行和单元格功能](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的选择模式](../../../../docs/framework/winforms/controls/selection-modes-in-the-windows-forms-datagridview-control.md)