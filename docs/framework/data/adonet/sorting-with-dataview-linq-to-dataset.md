---
title: "使用 DataView 进行排序 (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 885b3b7b-51c1-42b3-bb29-b925f4f69a6f
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 使用 DataView 进行排序 (LINQ to DataSet)
基于特定条件对数据进行排序，然后通过 UI 控件向客户端表示该数据的能力是数据绑定的一个重要特征。  <xref:System.Data.DataView> 提供多种方式对数据进行排序并返回按指定排序条件排序的数据行。  除了基于字符串的排序功能以外，<xref:System.Data.DataView> 还使您能够对排序条件使用 [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] 表达式。[!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 表达式允许执行比基于字符串的排序更复杂而功能更强大的排序操作。  本主题介绍这两种使用 <xref:System.Data.DataView> 的排序方法。  
  
## 通过具有排序信息的查询创建 DataView  
 可以通过 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询创建 <xref:System.Data.DataView> 对象。  如果查询包含 <xref:System.Linq.Enumerable.OrderBy%2A>、<xref:System.Linq.Enumerable.OrderByDescending%2A>、<xref:System.Linq.Enumerable.ThenBy%2A> 或 <xref:System.Linq.Enumerable.ThenByDescending%2A> 子句，则这些子句中的表达式将用作对 <xref:System.Data.DataView> 中的数据进行排序的基础。  例如，如果查询包含 `Order By…`和 `Then By…` 子句，则生成的 <xref:System.Data.DataView> 将按指定的两个列对数据进行排序。  
  
 基于表达式的排序具有比基于字符串的简单排序更强大、更复杂的排序功能。  请注意，基于字符串和基于表达式的排序是互相排斥的。  如果在通过查询创建 <xref:System.Data.DataView> 后设置基于字符串的 <xref:System.Data.DataView.Sort%2A>，则会清除从查询推断的基于表达式的筛选，并且无法重置。  
  
 创建 <xref:System.Data.DataView> 及修改任何排序或筛选信息时，均会生成 <xref:System.Data.DataView> 的索引。  通过在用于创建 <xref:System.Data.DataView> 的 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询中提供排序条件且在以后不修改排序信息，您可以获得最佳性能。  有关详细信息，请参阅[DataView 性能](../../../../docs/framework/data/adonet/dataview-performance.md)。  
  
> [!NOTE]
>  在大多数情况下，用于排序的表达式不应有副作用且必须是确定的。  另外，表达式不应包含依赖于固定执行次数的任何逻辑，因为排序操作可能会执行任意次。  
  
### 示例  
 下面的示例查询 SalesOrderHeader 表并按订单日期对返回的行排序，通过查询创建 <xref:System.Data.DataView>，并将 <xref:System.Data.DataView> 绑定到 <xref:System.Windows.Forms.BindingSource>。  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderby)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderby)]  
  
### 示例  
 下面的示例查询 SalesOrderHeader 表并按总应付金额对返回的行排序，通过查询创建 <xref:System.Data.DataView>，并将 <xref:System.Data.DataView> 绑定到 <xref:System.Windows.Forms.BindingSource>。  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderBy2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderby2)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderBy2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderby2)]  
  
### 示例  
 下面的示例查询 SalesOrderDetail 表并先按订单数量，然后按销售订单 ID 对返回的行排序，通过查询创建 <xref:System.Data.DataView>，并将 <xref:System.Data.DataView> 绑定到 <xref:System.Windows.Forms.BindingSource>。  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderByThenBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderbythenby)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderByThenBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderbythenby)]  
  
## 使用基于字符串的排序属性  
 <xref:System.Data.DataView> 的基于字符串的排序功能对于 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 仍有效。  通过 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询创建 <xref:System.Data.DataView> 后，可以使用 <xref:System.Data.DataView.Sort%2A> 属性对 <xref:System.Data.DataView>设置排序。  
  
 基于字符串和基于表达式的排序功能是互相排斥的。  设置 <xref:System.Data.DataView.Sort%2A> 属性将清除从创建 <xref:System.Data.DataView> 的查询中继承的基于表达式的排序。  
  
 有关基于字符串的 <xref:System.Data.DataView.Sort%2A> 筛选的更多信息，请参见[排序和筛选数据](../../../../docs/framework/data/adonet/dataset-datatable-dataview/sorting-and-filtering-data.md)。  
  
### 示例  
 下面的示例从 Contact 表创建 <xref:System.Data.DataView> 并先按姓氏以降序，然后按名字以升序对行进行排序：  
  
 [!code-csharp[DP DataView Samples#LDVStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvstringsort)]
 [!code-vb[DP DataView Samples#LDVStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvstringsort)]  
  
### 示例  
 下面的示例查询 Contact 表中以字母“S”开头的姓氏。  通过该查询创建 <xref:System.Data.DataView> 并将其绑定到 <xref:System.Windows.Forms.BindingSource> 对象。  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquerystringsort)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquerystringsort)]  
  
## 清除排序  
 有关 <xref:System.Data.DataView> 的排序信息可以在使用 <xref:System.Data.DataView.Sort%2A> 属性设置后清除。  清除 <xref:System.Data.DataView> 中的排序信息有两种方式：  
  
-   将 <xref:System.Data.DataView.Sort%2A> 属性设置为 `null`。  
  
-   将 <xref:System.Data.DataView.Sort%2A> 属性设置为一个空字符串。  
  
### 示例  
 下面的示例通过查询创建一个 <xref:System.Data.DataView> 并通过将 <xref:System.Data.DataView.Sort%2A> 属性设置为空字符串清除排序。  
  
 [!code-csharp[DP DataView Samples#LDVClearSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearsort)]
 [!code-vb[DP DataView Samples#LDVClearSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearsort)]  
  
### 示例  
 下面的示例从 Contact 表创建 <xref:System.Data.DataView> 并将 <xref:System.Data.DataView.Sort%2A> 属性设置为按姓氏以降序排序。  然后通过将 <xref:System.Data.DataView.Sort%2A> 属性设置为 `null` 来清除排序信息：  
  
 [!code-csharp[DP DataView Samples#LDVClearSort2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearsort2)]
 [!code-vb[DP DataView Samples#LDVClearSort2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearsort2)]  
  
## 请参阅  
 [数据绑定和 LINQ to DataSet](../../../../docs/framework/data/adonet/data-binding-and-linq-to-dataset.md)   
 [使用 DataView 进行筛选](../../../../docs/framework/data/adonet/filtering-with-dataview-linq-to-dataset.md)   
 [Sorting Data](../../../../ocs/visual-basic/programming-guide/concepts/linq/sorting-data.md)