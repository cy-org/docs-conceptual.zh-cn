---
title: "通过查询创建数据表 (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1b97afeb-03f8-41e2-8eb3-58aff65f7d18
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 通过查询创建数据表 (LINQ to DataSet)
数据绑定是 <xref:System.Data.DataTable> 对象的一种常用形式。  <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法接收查询结果并将数据复制到 <xref:System.Data.DataTable> 中，后者随后会使用该数据进行数据绑定。  在执行数据操作后，新的 <xref:System.Data.DataTable> 将合并回源 <xref:System.Data.DataTable>。  
  
 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法使用下面的过程来通过查询创建 <xref:System.Data.DataTable>：  
  
1.  <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法克隆源表中的 <xref:System.Data.DataTable>（实现 <xref:System.Linq.IQueryable%601> 接口的 <xref:System.Data.DataTable> 对象）。  <xref:System.Collections.IEnumerable> 源通常来源于 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 表达式或方法查询。  
  
2.  克隆的 <xref:System.Data.DataTable> 的架构从源表中枚举的第一个 <xref:System.Data.DataRow> 对象的列生成，克隆表的名称是源表的名称后面追加单词“query”。  
  
3.  对于源表中的每一行，会将行内容复制到新 <xref:System.Data.DataRow> 对象中，然后将该对象插入到克隆表中。  <xref:System.Data.DataRow.RowState%2A> 和 <xref:System.Data.DataRow.RowError%2A> 属性在整个复制操作过程中保留。  如果源中的 <xref:System.ArgumentException> 对象来自不同的表，则会引发 <xref:System.Data.DataRow>。  
  
4.  复制完可查询的输入表中的所有 <xref:System.Data.DataRow> 对象后，将返回克隆的 <xref:System.Data.DataTable>。  如果源序列不包含任何 <xref:System.Data.DataRow> 对象，则该方法将返回一个空 <xref:System.Data.DataTable>。  
  
 请注意，调用 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法将导致执行已绑定到源表的查询。  
  
 当 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法在源表的行中遇到空引用或可以为 null 的值类型时，它将用 <xref:System.DBNull.Value> 替换该值。  这样可以在返回的 <xref:System.Data.DataTable> 中正确处理 Null 值。  
  
 注意：<xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法接受可从多个 <xref:System.Data.DataTable> 或 <xref:System.Data.DataSet> 对象返回行的查询作为输入。  <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法将数据（不包括属性）从源 <xref:System.Data.DataTable> 或 <xref:System.Data.DataSet> 对象复制到返回的 <xref:System.Data.DataTable>。  您将需要显式设置返回的 <xref:System.Data.DataTable> 的属性，例如 <xref:System.Data.DataTable.Locale%2A> 和 <xref:System.Data.DataTable.TableName%2A>。  
  
 下面的示例查询 SalesOrderHeader 表中 2001 年 8 月 8 日以后的订单，并使用 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法通过查询创建 <xref:System.Data.DataTable>。  然后将 <xref:System.Data.DataTable> 绑定到作为 <xref:System.Windows.Forms.DataGridView> 的代理的 <xref:System.Windows.Forms.BindingSource>。  
  
 [!code-csharp[DP LINQ to DataSet Examples#CopyToDataTable1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#copytodatatable1)]
 [!code-vb[DP LINQ to DataSet Examples#CopyToDataTable1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#copytodatatable1)]  
  
## 创建自定义 CopyToDataTable\<T\> 方法  
 仅在 <xref:System.Collections.Generic.IEnumerable%601> 源上（其中泛型参数 `T` 类型为 <xref:System.Data.DataRow>）执行现有 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法。  虽然这十分有用，但是它并不允许从标量类型的序列、返回匿名类型的查询或执行表联接的查询来创建表。  有关如何实现两个从标量类型或匿名类型序列加载表自定义的 `CopyToDataTable` 方法的示例，请参见[如何：实现 CopyToDataTable\<T\>，其中泛型类型 T 不是 DataRow](../../../../docs/framework/data/adonet/implement-copytodatatable-where-type-not-a-datarow.md)。  
  
 本节的示例使用以下自定义类型：  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#ItemClass](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#itemclass)]
 [!code-vb[DP Custom CopyToDataTable Examples#ItemClass](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#itemclass)]  
  
### 示例  
 此示例在 `SalesOrderHeader` 和 `SalesOrderDetail` 表上执行联接以获得八月的联机订单，并从查询创建表。  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#Join](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#join)]
 [!code-vb[DP Custom CopyToDataTable Examples#Join](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#join)]  
  
### 示例  
 下面的示例查询价格高于 9.99 美元的商品集合，并从查询结果创建表。  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadItemsIntoTable](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loaditemsintotable)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadItemsIntoTable](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loaditemsintotable)]  
  
### 示例  
 下面的示例查询价格高于 9.99 的商品集合，并投影结果。  返回的匿名类型序列被加载到现有表中。  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadItemsIntoExistingTable](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loaditemsintoexistingtable)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadItemsIntoExistingTable](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loaditemsintoexistingtable)]  
  
### 示例  
 下面的示例查询价格高于 9.99 美元的商品集合，并投影结果。  返回的匿名类型序列被加载到现有表中。  表架构自动扩展，因为 `Book` 和 `Movies` 类型是从 `Item` 类型派生的。  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadItemsExpandSchema](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loaditemsexpandschema)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadItemsExpandSchema](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loaditemsexpandschema)]  
  
### 示例  
 下面的示例查询价格高于 9.99 美元的商品集合，并返回 <xref:System.Double> 的序列，它将被加载到新表中。  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadScalarSequence](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loadscalarsequence)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadScalarSequence](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loadscalarsequence)]  
  
## 请参阅  
 [编程指南](../../../../docs/framework/data/adonet/programming-guide-linq-to-dataset.md)   
 [泛型 Field 和 SetField 方法](../../../../docs/framework/data/adonet/generic-field-and-setfield-methods-linq-to-dataset.md)   
 [LINQ to DataSet 示例](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)