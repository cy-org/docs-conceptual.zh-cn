---
title: "表概述 | Microsoft Docs"
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
  - "文档, 表"
  - "流内容元素 [WPF], 表"
  - "表"
ms.assetid: 5e1105f4-8fc4-473a-ba55-88c8e71386e6
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 表概述
<xref:System.Windows.Documents.Table> 是一个块级元素，支持流文档内容的基于网格的表示。  此元素的灵活性极为有用，但该元素也由此变得更加复杂，从而难以理解和正确使用。  
  
 本主题包括以下部分。  
  
-   [表基础](#table_basics)  
  
-   [表与网格有什么区别？](#table_vs_Grid)  
  
-   [基本表结构](#basic_table_structure)  
  
-   [表包容](#table_containment)  
  
-   [行分组](#row_groupings)  
  
-   [背景呈现优先级](#rednering_precedence)  
  
-   [跨行或列](#spanning_rows_or_columns)  
  
-   [使用代码生成表](#building_a_table_with_code)  
  
-   [相关主题](#see_also)  
  
<a name="table_basics"></a>   
## 表基础  
  
<a name="table_vs_Grid"></a>   
### 表与网格有什么区别？  
 <xref:System.Windows.Documents.Table> 和 <xref:System.Windows.Controls.Grid> 共享某些通用功能，但二者分别最适用于不同的方案。  <xref:System.Windows.Documents.Table> 旨在在流内容内使用（有关流内容的更多信息，请参见[流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)）。  网格最适合在表单中（主要在流内容以外的任意位置）使用。  在 <xref:System.Windows.Documents.FlowDocument> 内，<xref:System.Windows.Documents.Table> 支持流内容行为（例如分页、列回流和内容选择），而 <xref:System.Windows.Controls.Grid> 则不支持这样的行为。  另一方面，<xref:System.Windows.Controls.Grid> 最适合在 <xref:System.Windows.Documents.FlowDocument> 之外使用，原因有多种，包括 <xref:System.Windows.Controls.Grid> 根据行和列索引添加元素，而 <xref:System.Windows.Documents.Table> 则不适合。  使用 <xref:System.Windows.Controls.Grid> 元素可以对子内容进行分层，从而允许多个元素共存于单个“单元格”内。<xref:System.Windows.Documents.Table> 不支持分层。  <xref:System.Windows.Controls.Grid> 的子元素可相对于其“单元格”边界区域进行绝对定位。  <xref:System.Windows.Documents.Table> 不支持此功能。  最后，相对于 <xref:System.Windows.Documents.Table>，<xref:System.Windows.Controls.Grid> 所需要的资源更少，因此，若要提高性能，请考虑使用 <xref:System.Windows.Controls.Grid>。  
  
<a name="basic_table_structure"></a>   
### 基本表结构  
 <xref:System.Windows.Documents.Table> 提供了一个基于网格的表示形式，包括列（由 <xref:System.Windows.Documents.TableColumn> 元素表示）和行（由 <xref:System.Windows.Documents.TableRow> 元素表示）。  <xref:System.Windows.Documents.TableColumn> 元素不承载内容，只是定义列和列的特征。  <xref:System.Windows.Documents.TableRow> 元素必须在 <xref:System.Windows.Documents.TableRowGroup> 元素中承载，该元素对表行的分组进行了定义。  <xref:System.Windows.Documents.TableCell> 元素（包含将要由表来表示的实际内容）必须在 <xref:System.Windows.Documents.TableRow> 元素中承载。  <xref:System.Windows.Documents.TableCell> 只能包含从 <xref:System.Windows.Documents.Block> 派生的元素。  <xref:System.Windows.Documents.TableCell> 有效的子元素包括：  
  
-   <xref:System.Windows.Documents.BlockUIContainer>  
  
-   <xref:System.Windows.Documents.List>  
  
-   <xref:System.Windows.Documents.Paragraph>  
  
-   <xref:System.Windows.Documents.Section>  
  
-   <xref:System.Windows.Documents.Table>  
  
> [!NOTE]
>  <xref:System.Windows.Documents.TableCell> 元素可能不会直接承载文本内容。  有关流内容元素（例如 <xref:System.Windows.Documents.TableCell>）的包容规则的更多信息，请参见[流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)。  
  
> [!NOTE]
>  <xref:System.Windows.Documents.Table> 与 <xref:System.Windows.Controls.Grid> 元素类似，但是它具有更多功能，因此需要更大的资源开销。  
  
 以下示例将使用 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 定义一个简单的 2 行 3 列的表。  
  
 [!code-xml[TableSnippets2#_Table_BasicLayout](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_basiclayout)]  
  
 下图显示了此示例的呈现效果。  
  
 ![屏幕快照：呈现一个基本表](../../../../docs/framework/wpf/advanced/media/basictablerrender.png "BasicTablerRender")  
  
<a name="table_containment"></a>   
### 表包容  
 <xref:System.Windows.Documents.Table> 派生自 <xref:System.Windows.Documents.Block> 元素，并遵循 <xref:System.Windows.Documents.Block> 级别元素的常见规则。  <xref:System.Windows.Documents.Table> 元素可以包含在以下任意元素中：  
  
-   <xref:System.Windows.Documents.FlowDocument>  
  
-   <xref:System.Windows.Documents.TableCell>  
  
-   <xref:System.Windows.Controls.ListBoxItem>  
  
-   <xref:System.Windows.Controls.ListViewItem>  
  
-   <xref:System.Windows.Documents.Section>  
  
-   <xref:System.Windows.Documents.Floater>  
  
-   <xref:System.Windows.Documents.Figure>  
  
<a name="row_groupings"></a>   
### 行分组  
 <xref:System.Windows.Documents.TableRowGroup> 元素提供了一种对表中的行进行任意分组的方式；表中的每行必须属于一个行分组。  行分组中的行通常具有相同的用途，并可作为一个组来设置样式。  行分组的一项常见应用是将特定用途的行（如标题行、标头和脚注行）与表中所含的主内容分隔开来。  
  
 以下示例使用 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 定义具有样式标头行和脚注行的表。  
  
 [!code-xml[TableSnippets2#_Table_RowGroups](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_rowgroups)]  
  
 下图显示了此示例的呈现效果。  
  
 ![屏幕快照：表行组](../../../../docs/framework/wpf/advanced/media/table-rowgroups.png "Table\_RowGroups")  
  
<a name="renderning_precedence"></a>   
### 背景呈现优先级  
 表元素以下列顺序呈现（[z 顺序](GTMT)从最低到最高）。  此顺序不能更改。  例如，这些元素不包含您可用于重写此已确定顺序的“z 顺序”属性。  
  
1.  <xref:System.Windows.Documents.Table>  
  
2.  <xref:System.Windows.Documents.TableColumn>  
  
3.  <xref:System.Windows.Documents.TableRowGroup>  
  
4.  <xref:System.Windows.Documents.TableRow>  
  
5.  <xref:System.Windows.Documents.TableCell>  
  
 请参考以下示例，该示例对表内每个元素的背景色进行了定义。  
  
 [!code-xml[TableSnippets2#_Table_ZOrder](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_zorder)]  
  
 下图显示了此示例的呈现方式（仅显示背景色）。  
  
 ![屏幕快照：表 z 顺序](../../../../docs/framework/wpf/advanced/media/table-zorder.png "Table\_ZOrder")  
  
<a name="spanning_rows_or_columns"></a>   
### 跨行或列  
 使用 <xref:System.Windows.Documents.TableCell.RowSpan%2A> 或 <xref:System.Windows.Documents.TableCell.ColumnSpan%2A> 特性，表单元格可分别配置为跨多行或多列。  
  
 请参考以下示例，该示例中有一个跨三列的单元格。  
  
 [!code-xml[TableSnippets2#_Table_ColumnSpan](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_columnspan)]  
  
 下图显示了此示例的呈现效果。  
  
 ![屏幕快照：跨全部三列的单元格](../../../../docs/framework/wpf/advanced/media/table-columnspan.png "Table\_ColumnSpan")  
  
<a name="building_a_table_with_code"></a>   
## 使用代码生成表  
 以下示例演示如何以编程方式创建 <xref:System.Windows.Documents.Table> 和填充其内容。  该表的内容分配到五个行（由 <xref:System.Windows.Documents.Table.RowGroups%2A> 对象中包含的 <xref:System.Windows.Documents.TableRow> 对象表示）和六个列（由 <xref:System.Windows.Documents.TableColumn> 对象表示）中。  各行用于不同的显示目的，其中，标题行用于显示整个表的标题，标头行用于描述表中数据的列，而脚注行则包含摘要信息。  请注意，“标题”、“标头”和“脚注”行并非表所固有的，它们只是具有不同特征的行。  表单元格包含实际内容，可以包括文本、图像或任何其他[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 元素。  
  
 首先，创建一个 <xref:System.Windows.Documents.FlowDocument> 以承载 <xref:System.Windows.Documents.Table>，并创建一个新的 <xref:System.Windows.Documents.Table>，同时将其添加到 <xref:System.Windows.Documents.FlowDocument> 内容中。  
  
 [!code-csharp[TableSnippets#_TableCreate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreate)]
 [!code-vb[TableSnippets#_TableCreate](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreate)]  
  
 然后，创建六个 <xref:System.Windows.Documents.TableColumn> 对象，并将它们添加到表的 <xref:System.Windows.Documents.Table.Columns%2A> 集合中，同时应用某些格式设置。  
  
> [!NOTE]
>  请注意，表的 <xref:System.Windows.Documents.Table.Columns%2A> 集合使用从零开始的标准索引。  
  
 [!code-csharp[TableSnippets#_TableCreateColumns](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreatecolumns)]
 [!code-vb[TableSnippets#_TableCreateColumns](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreatecolumns)]  
  
 然后，创建一个标题行，并将其添加到表中，同时应用一些格式设置。  标题行包含一个单元格，该单元格跨表中的全部六列。  
  
 [!code-csharp[TableSnippets#_TableAddTitleRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddtitlerow)]
 [!code-vb[TableSnippets#_TableAddTitleRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddtitlerow)]  
  
 然后，创建一个标头行并将其添加到表中，同时创建标头行中的单元格并填充其内容。  
  
 [!code-csharp[TableSnippets#_TableAddHeaderRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddheaderrow)]
 [!code-vb[TableSnippets#_TableAddHeaderRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddheaderrow)]  
  
 然后，创建一个数据行并将其添加到表中，同时创建此行中的单元格并填充其内容。  生成此行的过程与生成标头行的过程类似，只是应用的格式设置略有不同。  
  
 [!code-csharp[TableSnippets#_TableAddDataRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableadddatarow)]
 [!code-vb[TableSnippets#_TableAddDataRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableadddatarow)]  
  
 最后，创建、添加脚注行并设置其格式。  与标题行类似，该脚注包含一个跨表中全部六列的单元格。  
  
 [!code-csharp[TableSnippets#_TableAddFooterRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddfooterrow)]
 [!code-vb[TableSnippets#_TableAddFooterRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddfooterrow)]  
  
## 请参阅  
 [流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)   
 [使用 XAML 定义表](../../../../docs/framework/wpf/advanced/how-to-define-a-table-with-xaml.md)   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [使用流内容元素](../../../../docs/framework/wpf/advanced/how-to-use-flow-content-elements.md)