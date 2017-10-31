---
title: "如何：指定 Windows 窗体 DataGridView 控件的编辑模式 | Microsoft Docs"
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
  - "数据网格, 编辑模式"
  - "DataGridView 控件 [Windows 窗体], 编辑模式"
ms.assetid: 93e117e8-94c4-411b-ba31-645e475ed85c
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：指定 Windows 窗体 DataGridView 控件的编辑模式
默认情况下，用户可以通过在当前 <xref:System.Windows.Forms.DataGridView> 文本框单元格中键入或按 F2 键来编辑该单元格的内容。  当满足下面的所有条件时，单元格将进入编辑模式：  
  
-   能对基础数据源进行编辑。  
  
-   <xref:System.Windows.Forms.DataGridView> 控件已启用。  
  
-   <xref:System.Windows.Forms.DataGridView.EditMode%2A> 属性值不为 <xref:System.Windows.Forms.DataGridViewEditMode>。  
  
-   单元格、行、列和控件的 `ReadOnly` 属性都设置为 `false`。  
  
 在编辑模式中，用户可以更改单元格的值，并可按 Enter 键提交更改，或按 Esc 键将单元格恢复为其原始值。  
  
 可以配置 <xref:System.Windows.Forms.DataGridView> 控件，以使单元格在成为当前单元格时立即进入编辑模式。  在此情况下 Enter 和 Esc 键的行为不变，但在提交或恢复值后单元格保持在编辑模式中。  也可以配置控件，以使仅当用户在单元格中键入或仅当用户按 F2 键时，单元格才进入编辑模式。  最后，可以防止单元格进入编辑模式，除非调用 <xref:System.Windows.Forms.DataGridView.BeginEdit%2A> 方法。  
  
### 更改 DataGridView 控件的编辑模式  
  
-   将 <xref:System.Windows.Forms.DataGridView.EditMode%2A?displayProperty=fullName> 属性设置为适当的 <xref:System.Windows.Forms.DataGridViewEditMode> 枚举。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#067](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#067)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#067](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#067)]  
  
## 编译代码  
 此示例需要：  
  
-   名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件。  
  
-   对 <xref:System> 和 <xref:System.Windows.Forms> 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.EditMode%2A?displayProperty=fullName>   
 [Windows 窗体 DataGridView 控件中的数据输入](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)