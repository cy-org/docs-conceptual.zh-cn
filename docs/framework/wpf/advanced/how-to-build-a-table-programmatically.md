---
title: "如何：以编程方式生成表 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "创建, 表（以编程方式）"
  - "文档, 以编程方式创建表"
  - "表, 以编程方式创建"
ms.assetid: e3ca88f3-6e94-4b61-82fc-42104c10b761
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：以编程方式生成表
以下示例演示如何以编程方式创建 <xref:System.Windows.Documents.Table> 和填充其内容。  该表的内容分配到五个行（由 <xref:System.Windows.Documents.Table.RowGroups%2A> 对象中包含的 <xref:System.Windows.Documents.TableRow> 对象表示）和六个列（由 <xref:System.Windows.Documents.TableColumn> 对象表示）中。  各行用于不同的显示目的，其中，标题行用于显示整个表的标题，标头行用于描述表中数据的列，而脚注行则包含摘要信息。  请注意，“标题”、“标头”和“脚注”行并非表所固有的，它们只是具有不同特征的行。  表单元格包含实际内容，可以包括文本、图像或任何其他[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 元素。  
  
## 示例  
 首先，创建一个 <xref:System.Windows.Documents.FlowDocument> 以承载 <xref:System.Windows.Documents.Table>，并创建一个新的 <xref:System.Windows.Documents.Table>，同时将其添加到 <xref:System.Windows.Documents.FlowDocument> 内容中。  
  
 [!code-csharp[TableSnippets#_TableCreate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreate)]
 [!code-vb[TableSnippets#_TableCreate](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreate)]  
  
## 示例  
 然后，创建六个 <xref:System.Windows.Documents.TableColumn> 对象，并将它们添加到表的 <xref:System.Windows.Documents.Table.Columns%2A> 集合中，同时应用某些格式设置。  
  
> [!NOTE]
>  请注意，表的 <xref:System.Windows.Documents.Table.Columns%2A> 集合使用从零开始的标准索引。  
  
 [!code-csharp[TableSnippets#_TableCreateColumns](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreatecolumns)]
 [!code-vb[TableSnippets#_TableCreateColumns](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreatecolumns)]  
  
## 示例  
 然后，创建一个标题行，并将其添加到表中，同时应用一些格式设置。  标题行包含一个单元格，该单元格跨表中的全部六列。  
  
 [!code-csharp[TableSnippets#_TableAddTitleRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddtitlerow)]
 [!code-vb[TableSnippets#_TableAddTitleRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddtitlerow)]  
  
## 示例  
 然后，创建一个标头行并将其添加到表中，同时创建标头行中的单元格并填充其内容。  
  
 [!code-csharp[TableSnippets#_TableAddHeaderRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddheaderrow)]
 [!code-vb[TableSnippets#_TableAddHeaderRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddheaderrow)]  
  
## 示例  
 然后，创建一个数据行并将其添加到表中，同时创建此行中的单元格并填充其内容。  生成此行的过程与生成标头行的过程类似，只是应用的格式设置略有不同。  
  
 [!code-csharp[TableSnippets#_TableAddDataRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableadddatarow)]
 [!code-vb[TableSnippets#_TableAddDataRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableadddatarow)]  
  
## 示例  
 最后，创建、添加脚注行并设置其格式。  与标题行类似，该脚注包含一个跨表中全部六列的单元格。  
  
 [!code-csharp[TableSnippets#_TableAddFooterRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddfooterrow)]
 [!code-vb[TableSnippets#_TableAddFooterRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddfooterrow)]  
  
## 请参阅  
 [表概述](../../../../docs/framework/wpf/advanced/table-overview.md)