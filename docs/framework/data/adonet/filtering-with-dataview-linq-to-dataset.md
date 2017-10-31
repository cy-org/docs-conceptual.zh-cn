---
title: "使用 DataView 进行筛选 (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5632d74a-ff53-4ea7-9fe7-4a148eeb1c68
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 使用 DataView 进行筛选 (LINQ to DataSet)
使用特定条件筛选数据，然后通过 UI 控件在客户端中表示该数据的能力是数据绑定的一个重要特征。  <xref:System.Data.DataView> 提供多种方式来筛选数据并返回满足指定筛选条件的数据行子集。  除了基于字符串的筛选功能以外，<xref:System.Data.DataView> 还为筛选条件提供了使用 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 表达式的功能。[!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 表达式允许执行比基于字符串的筛选更复杂而功能更强大的筛选操作。  
  
 使用 <xref:System.Data.DataView> 筛选数据有两种方式：  
  
-   通过使用 Where 子句的 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询创建 <xref:System.Data.DataView>。  
  
-   使用 <xref:System.Data.DataView> 现有的基于字符串的筛选功能。  
  
## 通过具有筛选信息的查询创建 DataView  
 可以通过 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询创建 <xref:System.Data.DataView> 对象。  如果该查询包含一个 `Where` 子句，则会使用查询中的筛选信息创建 <xref:System.Data.DataView>。  `Where` 子句中的表达式用于确定哪些数据行将包括在 <xref:System.Data.DataView> 中并作为筛选器的基础。  
  
 基于表达式的筛选器具有比基于字符串的简单筛选器更强大、更复杂的筛选功能。  基于字符串的筛选器和基于表达式的筛选器是互相排斥的。  如果在通过查询创建 <xref:System.Data.DataView> 后设置基于字符串的 <xref:System.Data.DataView.RowFilter%2A>，则会清除从查询推断的基于表达式的筛选器。  
  
> [!NOTE]
>  在大多数情况下，用于筛选的表达式不应有副作用且必须是确定的。  另外，表达式不应包含依赖于固定执行次数的任何逻辑，因为筛选操作可能会执行任意次。  
  
### 示例  
 下面的示例查询 SalesOrderDetail 表中数量大于 2 且小于 6 的订单，通过查询创建 <xref:System.Data.DataView>，并将 <xref:System.Data.DataView> 绑定到 <xref:System.Windows.Forms.BindingSource>：  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhere](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhere)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhere](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhere)]  
  
### 示例  
 下面的示例通过查询 2001 年 6 月 6 日以后达成的订单来创建 <xref:System.Data.DataView>：  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhere3](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhere3)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhere3](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhere3)]  
  
### 示例  
 筛选也可以与排序组合使用。  下面的示例通过查询姓氏以“S”开始并按姓氏排序，然后按名字排序的联系人来创建 <xref:System.Data.DataView>：  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhereOrderByThenBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhereorderbythenby)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhereOrderByThenBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhereorderbythenby)]  
  
### 示例  
 下面的示例使用 SoundEx 算法查找姓氏与“Zhu”相近的联系人。  SoundEx 算法在 SoundEx 方法中实现。  
  
 [!code-csharp[DP DataView Samples#LDVSoundExFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvsoundexfilter)]
 [!code-vb[DP DataView Samples#LDVSoundExFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvsoundexfilter)]  
  
 SoundEx 是一种拼音算法，用于按英语发音来索引姓名，它最初由美国  人口调查局开发。  SoundEx 方法返回一个表示姓名的四字符代码，由一个英文字母后跟三个数字构成。  字母是姓名的首字母，数字对姓名中剩余的辅音字母编码。  发音相近的姓名具有相同的 SoundEx 代码。  上一示例的 SoundEx 方法中使用的 SoundEx 实现如下所示：  
  
 [!code-csharp[DP DataView Samples#SoundEx](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#soundex)]
 [!code-vb[DP DataView Samples#SoundEx](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#soundex)]  
  
## 使用 RowFilter 属性  
 <xref:System.Data.DataView> 现有的基于字符串的筛选功能仍可在 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 上下文中执行。  有关基于字符串的 <xref:System.Data.DataView.RowFilter%2A> 筛选的更多信息，请参见[排序和筛选数据](../../../../docs/framework/data/adonet/dataset-datatable-dataview/sorting-and-filtering-data.md)。  
  
 下面的示例从 Contact 表创建 <xref:System.Data.DataView>，然后设置 <xref:System.Data.DataView.RowFilter%2A> 属性以返回联系人的姓氏为“Zhu”的行：  
  
 [!code-csharp[DP DataView Samples#LDVRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvrowfilter)]
 [!code-vb[DP DataView Samples#LDVRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvrowfilter)]  
  
 从 <xref:System.Data.DataTable> 或 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询创建 <xref:System.Data.DataView> 后，可以使用 <xref:System.Data.DataView.RowFilter%2A> 属性基于行的列值指定行的子集。  基于字符串的筛选器和基于表达式的筛选器是互相排斥的。  设置 <xref:System.Data.DataView.RowFilter%2A> 属性将清除从 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询推断的筛选表达式，并且该筛选表达式无法重置。  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhereSetRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywheresetrowfilter)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhereSetRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywheresetrowfilter)]  
  
 如果要返回特定数据查询的结果而不是提供数据子集的动态视图，则可以使用 <xref:System.Data.DataView> 的 <xref:System.Data.DataView.Find%2A> 或 <xref:System.Data.DataView.FindRows%2A> 方法，而不设置 <xref:System.Data.DataView.RowFilter%2A> 属性。  <xref:System.Data.DataView.RowFilter%2A> 属性最适合用于用绑定控件显示筛选结果的数据绑定应用程序。  设置 <xref:System.Data.DataView.RowFilter%2A> 属性会重新生成数据的索引，从而增加应用程序的系统开销并降低性能。  <xref:System.Data.DataView.Find%2A> 和 <xref:System.Data.DataView.FindRows%2A> 方法使用当前索引，而不要求重新生成索引。  如果只想调用 <xref:System.Data.DataView.Find%2A> 或 <xref:System.Data.DataView.FindRows%2A> 一次，则应使用现有的 <xref:System.Data.DataView>。  如果想要调用 <xref:System.Data.DataView.Find%2A> 或 <xref:System.Data.DataView.FindRows%2A> 多次，则应该创建一个新的 <xref:System.Data.DataView> 以便对想要搜索的列重新生成索引，然后调用 <xref:System.Data.DataView.Find%2A> 或 <xref:System.Data.DataView.FindRows%2A> 方法。  有关 <xref:System.Data.DataView.Find%2A> 和 <xref:System.Data.DataView.FindRows%2A> 方法的更多信息，请参见[查找行](../../../../docs/framework/data/adonet/dataset-datatable-dataview/finding-rows.md)和 [DataView 性能](../../../../docs/framework/data/adonet/dataview-performance.md)。  
  
## 清除筛选器  
 使用 <xref:System.Data.DataView.RowFilter%2A> 属性设置筛选之后，可以清除 <xref:System.Data.DataView> 上的筛选器。  <xref:System.Data.DataView> 上的筛选器可以采用两种不同的方式清除：  
  
-   将 <xref:System.Data.DataView.RowFilter%2A> 属性设置为 `null`。  
  
-   将 <xref:System.Data.DataView.RowFilter%2A> 属性设置为一个空字符串。  
  
### 示例  
 下面的示例通过查询创建 <xref:System.Data.DataView>，然后通过将 <xref:System.Data.DataView.RowFilter%2A> 属性设置为 `null` 来清除该筛选器：  
  
 [!code-csharp[DP DataView Samples#LDVClearRowFilter2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearrowfilter2)]
 [!code-vb[DP DataView Samples#LDVClearRowFilter2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearrowfilter2)]  
  
### 示例  
 下面的示例从表创建 <xref:System.Data.DataView>，设置 <xref:System.Data.DataView.RowFilter%2A> 属性，然后通过将 <xref:System.Data.DataView.RowFilter%2A> 属性设置为一个空的字符串来清除该筛选器：  
  
 [!code-csharp[DP DataView Samples#LDVClearRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearrowfilter)]
 [!code-vb[DP DataView Samples#LDVClearRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearrowfilter)]  
  
## 请参阅  
 [数据绑定和 LINQ to DataSet](../../../../docs/framework/data/adonet/data-binding-and-linq-to-dataset.md)   
 [使用 DataView 进行排序](../../../../docs/framework/data/adonet/sorting-with-dataview-linq-to-dataset.md)