---
title: "查询示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 137f8677-494c-4d49-95ce-c17742f2d01f
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 查询示例
本节提供典型的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 查询的 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 和 C\# 示例。  使用 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 的开发人员可以在“示例”一节中提供的示例解决方案中找到许多其他示例。  有关详细信息，请参阅[示例](../../../../../../docs/framework/data/adonet/sql/linq/samples.md)。  
  
> [!IMPORTANT]
>  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 文档中的代码示例中经常会用到 db。  假定 db 是继承自 <xref:System.Data.Linq.DataContext> 的 Northwind 类的一个实例。  
  
## 本节内容  
 [聚合查询](../../../../../../docs/framework/data/adonet/sql/linq/aggregate-queries.md)  
 介绍如何使用 <xref:System.Linq.Enumerable.Average%2A>、<xref:System.Linq.Enumerable.Count%2A> 等。  
  
 [返回序列中的第一个元素](../../../../../../docs/framework/data/adonet/sql/linq/return-the-first-element-in-a-sequence.md)  
 提供使用 <xref:System.Linq.Enumerable.First%2A> 的示例。  
  
 [返回或跳过序列中的元素](../../../../../../docs/framework/data/adonet/sql/linq/return-or-skip-elements-in-a-sequence.md)  
 提供使用 <xref:System.Linq.Enumerable.Take%2A> 和 <xref:System.Linq.Enumerable.Skip%2A> 的示例。  
  
 [对序列中的元素进行排序](../../../../../../docs/framework/data/adonet/sql/linq/sort-elements-in-a-sequence.md)  
 提供使用 <xref:System.Linq.Enumerable.OrderBy%2A> 的示例。  
  
 [对序列中的元素进行分组](../../../../../../docs/framework/data/adonet/sql/linq/group-elements-in-a-sequence.md)  
 提供使用 <xref:System.Linq.Enumerable.GroupBy%2A> 的示例。  
  
 [从序列中消除重复元素](../../../../../../docs/framework/data/adonet/sql/linq/eliminate-duplicate-elements-from-a-sequence.md)  
 提供使用 <xref:System.Linq.Enumerable.Distinct%2A> 的示例。  
  
 [确定序列中的元素是否部分或全部满足条件](../../../../../../docs/framework/data/adonet/sql/linq/determine-if-any-or-all-elements-in-a-sequence-satisfy-a-condition.md)  
 提供使用 <xref:System.Linq.Enumerable.All%2A> 和 <xref:System.Linq.Enumerable.Any%2A> 的示例。  
  
 [串联两个序列](../../../../../../docs/framework/data/adonet/sql/linq/concatenate-two-sequences.md)  
 提供使用 <xref:System.Linq.Enumerable.Concat%2A> 的示例。  
  
 [返回两个序列之间的差集](../../../../../../docs/framework/data/adonet/sql/linq/return-the-set-difference-between-two-sequences.md)  
 提供使用 <xref:System.Linq.Enumerable.Except%2A> 的示例。  
  
 [返回两个序列的交集](../../../../../../docs/framework/data/adonet/sql/linq/return-the-set-intersection-of-two-sequences.md)  
 提供使用 <xref:System.Linq.Enumerable.Intersect%2A> 的示例。  
  
 [返回两个序列的并集](../../../../../../docs/framework/data/adonet/sql/linq/return-the-set-union-of-two-sequences.md)  
 提供使用 <xref:System.Linq.Enumerable.Union%2A> 的示例。  
  
 [将序列转换为数组](../../../../../../docs/framework/data/adonet/sql/linq/convert-a-sequence-to-an-array.md)  
 提供使用 <xref:System.Linq.Enumerable.ToArray%2A> 的示例。  
  
 [将序列转换为泛型列表](../../../../../../docs/framework/data/adonet/sql/linq/convert-a-sequence-to-a-generic-list.md)  
 提供使用 <xref:System.Linq.Enumerable.ToList%2A> 的示例。  
  
 [将类型转换为泛型 IEnumerable](../../../../../../docs/framework/data/adonet/sql/linq/convert-a-type-to-a-generic-ienumerable.md)  
 提供使用 <xref:System.Linq.Enumerable.AsEnumerable%2A> 的示例。  
  
 [构建联接和叉积查询](../../../../../../docs/framework/data/adonet/sql/linq/formulate-joins-and-cross-product-queries.md)  
 提供在 `from`、`where` 和 `select` 子句中使用外键导航的示例。  
  
 [构建投影](../../../../../../docs/framework/data/adonet/sql/linq/formulate-projections.md)  
 提供通过结合使用 `select` 和其他功能（如匿名类型）构建查询投影的示例。  
  
## 相关章节  
 [Standard Query Operators Overview](../../../../../../ocs/visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)  
 解释标准查询运算符的概念。  
  
 [查询概念](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)  
 解释 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 如何使用适用于查询的概念。  
  
 [编程指南](../../../../../../docs/framework/data/adonet/sql/linq/programming-guide.md)  
 提供用于访问一些主题的门户，这些主题解释了与 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 相关的编程概念。