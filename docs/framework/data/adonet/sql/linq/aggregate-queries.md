---
title: "聚合查询 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 13ec5580-05ce-4a1f-9d3d-8660be7891a2
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 聚合查询
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支持 `Average`、`Count`、`Max`、`Min` 和 `Sum` 聚合运算符。  请注意 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中聚合运算符的以下特征：  
  
-   聚合查询是立即执行的。  
  
     有关详细信息，请参阅[Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md)。  
  
-   聚合查询通常返回一个数字，而非一个集合。  
  
     有关详细信息，请参阅[Aggregation Operations](../../../../../../ocs/visual-basic/programming-guide/concepts/linq/aggregation-operations.md)。  
  
-   不能对匿名类型调用聚合。  
  
 以下主题中的示例来自 Northwind 示例数据库。  有关详细信息，请参阅[下载示例数据库](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)。  
  
## 本节内容  
 [返回数值序列的平均值](../../../../../../docs/framework/data/adonet/sql/linq/return-the-average-value-from-a-numeric-sequence.md)  
 演示如何使用 <xref:System.Linq.Enumerable.Average%2A> 运算符。  
  
 [对序列中的元素进行计数](../../../../../../docs/framework/data/adonet/sql/linq/count-the-number-of-elements-in-a-sequence.md)  
 演示如何使用 <xref:System.Linq.Enumerable.Count%2A> 运算符。  
  
 [查找数值序列中的最大值](../../../../../../docs/framework/data/adonet/sql/linq/find-the-maximum-value-in-a-numeric-sequence.md)  
 演示如何使用 <xref:System.Linq.Enumerable.Max%2A> 运算符。  
  
 [查找数值序列中的最小值](../../../../../../docs/framework/data/adonet/sql/linq/find-the-minimum-value-in-a-numeric-sequence.md)  
 演示如何使用 <xref:System.Linq.Enumerable.Min%2A> 运算符。  
  
 [计算数值序列中的值之和](../../../../../../docs/framework/data/adonet/sql/linq/compute-the-sum-of-values-in-a-numeric-sequence.md)  
 演示如何使用 <xref:System.Linq.Enumerable.Sum%2A> 运算符。  
  
## 相关章节  
 [查询示例](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)  
 提供指向 Visual Basic 和 C\# 中 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 查询的链接。  
  
 [查询概念](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)  
 提供指向特定主题的链接，这些主题解释有关在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中设计 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 查询的一些概念。  
  
 [Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md)  
 解释 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 中查询的工作原理。