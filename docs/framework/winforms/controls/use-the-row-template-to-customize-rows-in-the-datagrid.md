---
title: "如何：使用行模板自定义 Windows 窗体 DataGridView 控件中的行 | Microsoft Docs"
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
  - "数据网格, 自定义行"
  - "DataGridView 控件 [Windows 窗体], 自定义行"
ms.assetid: 6db61607-7e57-4a84-8d63-9d6a7ed7f9ff
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用行模板自定义 Windows 窗体 DataGridView 控件中的行
<xref:System.Windows.Forms.DataGridView> 控件以行模板为基础，通过数据绑定或在不指定要使用的现有行的情况下调用 <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A?displayProperty=fullName> 方法向控件中添加行。  
  
 与 <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A> 属性相比，行模板能更好地控制行的外观和行为。  使用行模板，可以设置包括 <xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A> 在内的任何 <xref:System.Windows.Forms.DataGridViewRow> 属性。  
  
 在有些情况中，必须使用行模板才能达到特殊效果。  例如，不能在 <xref:System.Windows.Forms.DataGridViewCellStyle> 中存储行高信息，因此必须使用行模板来更改所有行使用的默认高度。  当您创建从 <xref:System.Windows.Forms.DataGridViewRow> 派生的自己的类，并在向该控件添加新行时要使用自定义类型时，行模板也十分有用。  
  
> [!NOTE]
>  只在添加行时使用行模板。  不能通过更改行模板来更改现有行。  
  
### 使用行模板  
  
-   在从 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A?displayProperty=fullName> 属性检索到的对象上设置属性。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.RowTemplate#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.RowTemplate/CPP/datagridviewrowtemplate.cpp#1)]
     [!code-csharp[System.Windows.Forms.DataGridView.RowTemplate#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.RowTemplate/CS/datagridviewrowtemplate.cs#1)]
     [!code-vb[System.Windows.Forms.DataGridView.RowTemplate#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.RowTemplate/VB/datagridviewrowtemplate.vb#1)]  
  
## 编译代码  
 此示例需要：  
  
-   名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件。  
  
-   对 <xref:System?displayProperty=fullName>、<xref:System.Drawing?displayProperty=fullName> 和 <xref:System.Windows.Forms?displayProperty=fullName> 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 <xref:System.Windows.Forms.DataGridViewRow>   
 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A?displayProperty=fullName>   
 [Windows 窗体 DataGridView 控件中的基本格式设置和样式设置](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)