---
title: "Null 比较 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: ef88af8c-8dfe-4556-8b56-81df960a900b
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Null 比较
数据源中的 `null` 值指示未知的值。  在 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 查询中，可以检查 null 值以便仅对具有有效（非 null）数据的行执行特定的计算或比较。  但是，CLR null 语义可能与数据源的 null 语义不同。  大多数数据库使用某个版本的三值逻辑处理 null 比较。  即，对 null 值的比较不会计算为 `true` 或 `false`，而是计算为 `unknown`。  通常这是 ANSI null 值的实现，但情况并非总是如此。  
  
 在 SQL Server 中，null 等于 null 比较默认返回 null 值。  在下面的示例中，`ShipDate` 为 null 的行会从结果集中排除，[!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] 语句返回 0 行。  
  
```  
-- Find order details and orders with no ship date.  
SELECT h.SalesOrderID  
FROM Sales.SalesOrderHeader h  
JOIN Sales.SalesOrderDetail o ON o.SalesOrderID = h.SalesOrderID  
WHERE h.ShipDate IS Null  
```  
  
 这与 CLR null 语义有很大差异，在 CLR null 语义中 null 等于 null 比较返回 true。  
  
 下面的 LINQ 查询以 CLR 表示，但在数据源中执行。  由于无法保证在数据源中会遵循 CLR 语义，因此预期行为是不确定的。  
  
 [!code-csharp[DP L2E Conceptual Examples#JoinOnNull](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#joinonnull)]
 [!code-vb[DP L2E Conceptual Examples#JoinOnNull](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#joinonnull)]  
  
## 键选择器  
 “键选择器”是在标准查询运算符中用于从元素提取键的函数。  在键选择器函数中，表达式可以与常量进行比较。  如果表达式与 null 常量进行比较或两个 null 常量进行比较，则会展现 CLR null 语义。  如果数据源中具有 null 值的两个列进行比较，则会展现存储 null 语义。  键选择器出现在许多分组和排序标准查询运算符（如 <xref:System.Linq.Queryable.GroupBy%2A>）中，用于选择对查询结果进行排序或分组所依据的键。  
  
## Null 对象上的 Null 属性  
 在 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 中，null 对象的属性为 null。  当尝试引用 CLR 中的 null 对象的属性时，会收到 <xref:System.NullReferenceException>。  当 LINQ 查询涉及 null 对象的属性时，可能会导致不一致的行为。  
  
 例如，下面的查询在命令树层中执行对 `NewProduct` 的强制转换，这可能导致 `Introduced` 属性为 null。  如果数据库将 null 比较定义为 <xref:System.DateTime> 比较计算为 true，则会包含该行。  
  
 [!code-csharp[DP L2E Conceptual Examples#CastResultsIsNull](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#castresultsisnull)]
 [!code-vb[DP L2E Conceptual Examples#CastResultsIsNull](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#castresultsisnull)]  
  
## 将 Null 集合传递到聚合函数  
 在 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 中，当您将支持 `IQueryable` 的集合传递到聚合函数时，将在数据库中执行聚合运算。  在内存中执行的查询的结果与在数据库中执行的查询的结果可能有差异。  对于内存中查询，如果没有匹配项，查询将返回零。  在数据库中，同一查询返回 `null`。  如果将 `null` 值传递到 LINQ 聚合函数，将引发异常。  若要接受可能的 `null` 值，请将类型和接收查询结果的类型的属性强制转换为可以为 null 的类型。  
  
## 请参阅  
 [LINQ to Entities 查询中的表达式](../../../../../../docs/framework/data/adonet/ef/language-reference/expressions-in-linq-to-entities-queries.md)