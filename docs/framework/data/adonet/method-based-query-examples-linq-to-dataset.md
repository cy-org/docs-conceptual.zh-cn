---
title: "基于方法的查询示例 (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d340775c-7f39-4087-a290-5cbec6cfa68e
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 基于方法的查询示例 (LINQ to DataSet)
本节提供使用标准查询运算符的基于方法的查询语法中的 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 编程示例。  这些示例中所使用的 <xref:System.Data.DataSet> 已通过使用 [向数据集中加载数据](../../../../docs/framework/data/adonet/loading-data-into-a-dataset.md) 中指定的 `FillDataSet` 方法进行填充。  有关详细信息，请参阅[Standard Query Operators Overview](../../../../ocs/visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
## 本节内容  
 [投影](../../../../docs/framework/data/adonet/method-based-query-syntax-examples-projection.md)  
 本主题中的示例演示如何使用 <xref:System.Linq.Enumerable.Select%2A> 和 <xref:System.Linq.Enumerable.SelectMany%2A> 方法来查询 <xref:System.Data.DataSet>。  
  
 [分区](../../../../docs/framework/data/adonet/method-based-query-syntax-examples-partitioning-linq.md)  
 本主题中的示例演示如何使用 <xref:System.Linq.Enumerable.Skip%2A> 和 <xref:System.Linq.Enumerable.Take%2A> 方法来查询 <xref:System.Data.DataSet> 并分隔结果。  
  
 [Ordering](../../../../docs/framework/data/adonet/method-based-query-syntax-examples-ordering-linq-to-dataset.md)  
 本主题中的示例演示如何使用 <xref:System.Linq.Enumerable.OrderBy%2A>、<xref:System.Linq.Enumerable.OrderByDescending%2A>、<xref:System.Linq.Enumerable.Reverse%2A> 和 <xref:System.Linq.Enumerable.ThenByDescending%2A> 方法来查询 <xref:System.Data.DataSet> 并排序结果。  
  
 [集合运算符](../../../../docs/framework/data/adonet/method-based-query-syntax-examples-set-operators.md)  
 本主题中的示例演示如何使用 <xref:System.Linq.Enumerable.Distinct%2A>、<xref:System.Linq.Enumerable.Except%2A>、<xref:System.Linq.Enumerable.Intersect%2A> 和 <xref:System.Linq.Enumerable.Union%2A> 运算符对多组数据行执行基于值的比较运算。  
  
 [转换运算符](../../../../docs/framework/data/adonet/method-based-query-syntax-examples-conversion-operators.md)  
 本主题中的示例演示如何使用 <xref:System.Linq.Enumerable.ToArray%2A>、<xref:System.Linq.Enumerable.ToDictionary%2A> 和 <xref:System.Linq.Enumerable.ToList%2A> 方法立即执行查询表达式。  
  
 [元素运算符](../../../../docs/framework/data/adonet/method-based-query-syntax-examples-element-operators.md)  
 本主题中的示例演示如何使用 <xref:System.Linq.Enumerable.First%2A> 和 <xref:System.Linq.Enumerable.ElementAt%2A> 方法来获取 <xref:System.Data.DataSet> 中的 <xref:System.Data.DataRow> 元素。  
  
 [聚合运算符](../../../../docs/framework/data/adonet/method-based-query-syntax-examples-aggregate-operators.md)  
 本主题中的示例演示如何使用 <xref:System.Linq.Enumerable.Average%2A>、<xref:System.Linq.Enumerable.Count%2A>、<xref:System.Linq.Enumerable.Max%2A>、<xref:System.Linq.Enumerable.Min%2A> 和 <xref:System.Linq.Enumerable.Sum%2A> 方法来查询 <xref:System.Data.DataSet> 并聚合数据。  
  
 [Join](../../../../docs/framework/data/adonet/method-based-query-syntax-examples-join-linq-to-dataset.md)  
 本主题中的示例演示如何使用 <xref:System.Linq.Enumerable.GroupJoin%2A> 和 <xref:System.Linq.Enumerable.Join%2A> 方法来查询 <xref:System.Data.DataSet>。  
  
## 请参阅  
 [查询表达式示例：](../../../../docs/framework/data/adonet/query-expression-examples-linq-to-dataset.md)   
 [数据集特定的运算符示例](../../../../docs/framework/data/adonet/dataset-specific-operator-examples-linq-to-dataset.md)   
 [LINQ to DataSet 示例](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)