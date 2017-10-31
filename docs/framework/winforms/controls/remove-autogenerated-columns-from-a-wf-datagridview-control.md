---
title: "如何：从 Windows 窗体 DataGridView 控件中移除自动生成的列 | Microsoft Docs"
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
  - "列 [Windows 窗体], 移除"
  - "DataGridView 控件 [Windows 窗体], 移除列"
ms.assetid: 92e28d98-95a3-446c-9150-41b7c7e5be15
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：从 Windows 窗体 DataGridView 控件中移除自动生成的列
如果将 <xref:System.Windows.Forms.DataGridView> 控件设置为根据其数据源中的数据自动生成列，则可以选择忽略某些列。  可以通过调用 <xref:System.Windows.Forms.DataGridView.Columns%2A> 集合的 <xref:System.Windows.Forms.DataGridViewColumnCollection.Remove%2A> 方法进行此操作。  或者，也可通过将 <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A> 属性设置为 `false` 来隐藏列。  当要在某些情况下显示隐藏的列或需要访问未显示的列中的数据时，此方法很有用。  
  
### 移除自动生成的列  
  
-   调用 <xref:System.Windows.Forms.DataGridView.Columns%2A> 集合的 <xref:System.Windows.Forms.DataGridViewColumnCollection.Remove%2A> 方法。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#111](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#111)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#111](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#111)]  
  
### 隐藏自动生成的列  
  
-   将列的 <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A> 属性设置为 `false`。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#112](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#112)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#112](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#112)]  
  
## 示例  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#110](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#110)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#110](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#110)]  
  
## 编译代码  
 此示例需要：  
  
-   一个名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件，该控件绑定到包含 `Fax` 和 `CustomerID` 列的表（如 Northwind 示例数据库中的 `Customers` 表）。  
  
-   对 <xref:System?displayProperty=fullName> 和 <xref:System.Windows.Forms?displayProperty=fullName> 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.AutoGenerateColumns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.Columns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumnCollection.Remove%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A?displayProperty=fullName>   
 [在 Windows 窗体 DataGridView 控件中显示数据](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)