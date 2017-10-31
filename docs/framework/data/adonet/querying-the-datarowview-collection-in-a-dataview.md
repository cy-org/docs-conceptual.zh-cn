---
title: "在 DataView 中查询 DataRowView 集合 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b9070a12-1094-44d6-bb87-a23b50bcb0af
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 在 DataView 中查询 DataRowView 集合
<xref:System.Data.DataView> 公开了 <xref:System.Data.DataRowView> 对象的可枚举集合。  <xref:System.Data.DataRowView> 表示 <xref:System.Data.DataRow> 的自定义视图，并在控件中显示特定版本的 <xref:System.Data.DataRow>。  只有一种版本的 <xref:System.Data.DataRow> 可通过控件显示，例如 <xref:System.Windows.Forms.DataGridView>。  您可以通过 <xref:System.Data.DataRowView> 的 <xref:System.Data.DataRowView.Row%2A> 属性访问 <xref:System.Data.DataRowView> 公开的 <xref:System.Data.DataRow>。  当使用 <xref:System.Data.DataRowView> 查看值时，<xref:System.Data.DataView.RowStateFilter%2A> 属性决定公开基础 <xref:System.Data.DataRow> 的哪个行版本。  有关使用 <xref:System.Data.DataRow> 访问不同行版本的信息，请参见[行状态与行版本](../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)。  因为 <xref:System.Data.DataView> 公开的 <xref:System.Data.DataRowView> 对象的集合是可枚举的，所以您可以使用 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 对它执行查询。  
  
 下面的示例对 `Product` 表执行查询查找红色的产品，并从该查询创建表。  从该表创建 <xref:System.Data.DataView> 并将 <xref:System.Data.DataView.RowStateFilter%2A> 属性设置为筛选已删除和修改的行。  然后将 <xref:System.Data.DataView> 用作 LINQ 查询中的源，并将已修改和删除的 <xref:System.Data.DataRowView> 对象绑定到 <xref:System.Windows.Forms.DataGridView> 控件。  
  
 [!code-csharp[DP DataView Samples#QueryDataView2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#querydataview2)]
 [!code-vb[DP DataView Samples#QueryDataView2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#querydataview2)]  
  
 下面的示例从绑定到 <xref:System.Windows.Forms.DataGridView> 控件的视图创建了一个产品表。  对 <xref:System.Data.DataView> 进行查询查找红色的产品，并将排序的结果绑定到 <xref:System.Windows.Forms.DataGridView> 控件。  
  
 [!code-csharp[DP DataView Samples#QueryDataView1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#querydataview1)]
 [!code-vb[DP DataView Samples#QueryDataView1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#querydataview1)]  
  
## 请参阅  
 [数据绑定和 LINQ to DataSet](../../../../docs/framework/data/adonet/data-binding-and-linq-to-dataset.md)