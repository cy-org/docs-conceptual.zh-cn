---
title: "从标识缓存中检索对象 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 96c13903-ccb6-4a0e-ab6a-8ca955ca314d
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 从标识缓存中检索对象
本主题介绍从 <xref:System.Data.Linq.DataContext> 管理的标识缓存中返回对象的 LINQ to SQL 查询类型。  
  
 在 LINQ to SQL 中，<xref:System.Data.Linq.DataContext> 管理对象的一种方法是在执行查询时将对象标识记录到标识缓存中。  在有些情况下，LINQ to SQL 将先尝试从标识缓存中检索对象，然后再在数据库中执行查询。  
  
 通常，如果 LINQ to SQL 查询要从标识缓存中返回对象，该查询必须基于对象的主键，并且必须返回单一对象。  特别是，该查询必须具有下面显示的常规形式之一。  
  
> [!NOTE]
>  预编译的查询不会从标识缓存中返回对象。  有关预编译查询的更多信息，请参见 <xref:System.Data.Linq.CompiledQuery> 和[如何：存储和重用查询](../../../../../../docs/framework/data/adonet/sql/linq/how-to-store-and-reuse-queries.md)。  
  
 查询必须具有以下常规形式之一，才能从标识缓存中检索对象：  
  
-   <xref:System.Data.Linq.Table%601> `.Function1(` `predicate` `)`  
  
-   <xref:System.Data.Linq.Table%601> `.Function1(` `predicate` `).Function2()`  
  
 在这些常规形式中，`Function1`、`Function2` 和 `predicate` 定义如下。  
  
 `Function1` 可以是以下任意形式：  
  
-   <xref:System.Linq.Queryable.Where%2A>  
  
-   <xref:System.Linq.Queryable.First%2A>  
  
-   <xref:System.Linq.Queryable.FirstOrDefault%2A>  
  
-   <xref:System.Linq.Queryable.Single%2A>  
  
-   <xref:System.Linq.Queryable.SingleOrDefault%2A>  
  
 `Function2` 可以是以下任意形式：  
  
-   <xref:System.Linq.Queryable.First%2A>  
  
-   <xref:System.Linq.Queryable.FirstOrDefault%2A>  
  
-   <xref:System.Linq.Queryable.Single%2A>  
  
-   <xref:System.Linq.Queryable.SingleOrDefault%2A>  
  
 `predicate` 必须是一个表达式，并且其中对象的主键属性必须设置为常量值。  如果对象的主键由多个属性定义，则每个主键属性都必须设置为常量值。  下面的示例是 `predicate` 必须采用的形式：  
  
-   `c => c.PK == constant_value`  
  
-   `c => c.PK1 == constant_value1 && c=> c.PK2 == constant_value2`  
  
## 示例  
 下面的代码提供了从标识缓存中检索对象的 LINQ to SQL 查询类型的示例。  
  
 [!code-csharp[L2S_QueryCache#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/l2s_querycache/cs/program.cs#1)]
 [!code-vb[L2S_QueryCache#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/l2s_querycache/vb/module1.vb#1)]  
  
## 请参阅  
 [查询概念](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)   
 [对象标识](../../../../../../docs/framework/data/adonet/sql/linq/object-identity.md)   
 [背景信息](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)   
 [对象标识](../../../../../../docs/framework/data/adonet/sql/linq/object-identity.md)