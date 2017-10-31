---
title: "如何：为 Windows 窗体 DataGridView 控件中的新行指定默认值 | Microsoft Docs"
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
  - "数据网格, 新行的默认值"
  - "DataGridView 控件 [Windows 窗体], 数据输入"
  - "DataGridView 控件 [Windows 窗体], 新行的默认值"
  - "行, 指定默认值"
ms.assetid: 8d127963-d9f8-4e4e-9f7f-beb66688f1f2
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：为 Windows 窗体 DataGridView 控件中的新行指定默认值
当应用程序为新添加的行填充默认值时，能使数据输入变得更方便。  通过 <xref:System.Windows.Forms.DataGridView> 类，可以使用 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded> 事件填充默认值。  此事件在用户进入新记录的行时引发。  在代码处理此事件时，可以用选择的值填充所需的单元格。  
  
 下面的代码示例演示如何使用 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded> 事件指定新行的默认值。  
  
## 示例  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#120](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#120)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#120](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#120)]  
  
## 编译代码  
 此示例需要：  
  
-   名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件。  
  
-   `NewCustomerId` 函数，用于生成唯一的 `CustomerID` 值。  
  
-   对 <xref:System?displayProperty=fullName> 和 <xref:System.Windows.Forms?displayProperty=fullName> 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded?displayProperty=fullName>   
 [Windows 窗体 DataGridView 控件中的数据输入](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)   
 [在 Windows 窗体 DataGridView 控件中使用新记录行](../../../../docs/framework/winforms/controls/using-the-row-for-new-records-in-the-windows-forms-datagridview-control.md)