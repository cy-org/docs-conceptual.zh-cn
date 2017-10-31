---
title: "LINQ to Entities 中的查询 | Microsoft Docs"
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
ms.assetid: c015a609-29eb-4e95-abb1-2ca721c6e2ad
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# LINQ to Entities 中的查询
查询是一种从数据源检索数据的表达式。  查询通常用专用查询语言表示，如用于关系数据库的 SQL 和用于 XML 的 XQuery。  因此，开发人员对于他们查询的每种类型的数据源或数据格式，都不得不学习一种新的查询语言。  语言集成查询 \(LINQ\) 为跨各种数据源和格式处理数据提供了一种更简单的、一致的模型。  在 LINQ 查询中，您始终可以使用编程对象。  
  
 LINQ 查询操作包含三个操作：获得一个或多个数据源、创建查询并执行查询。  
  
 可以通过 LINQ 查询实现 <xref:System.Collections.Generic.IEnumerable%601> 泛型接口或 <xref:System.Linq.IQueryable%601> 泛型接口的数据源。  <xref:System.Data.Objects.ObjectQuery%601> 泛型类（可实现 <xref:System.Linq.IQueryable%601> 泛型接口）的实例可充当 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 查询的数据源。  <xref:System.Data.Objects.ObjectQuery%601> 泛型类表示一个查询，该查询返回零个或多个类型化对象的集合。  您还可以通过使用 C\# 关键字 `var`（在 Visual Basic 中为 Dim）让编译器推断实体的类型。  
  
 在查询中，您可以确切指定要从数据源检索哪些信息。  查询也可以指定返回信息之前信息的排序、分组和表现方式。  在 LINQ 中，查询存储在变量中。  如果查询返回一系列值，则查询变量本身必须为可查询的类型。  此查询变量不执行任何操作，也不返回任何数据；它只存储查询信息。  创建查询后必须执行该查询以检索任何数据。  
  
## 查询语法  
 可以通过两种不同的语法编写 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 查询：查询表达式语法和基于方法的查询语法。  查询表达式语法是 C\# 3.0 和 Visual Basic 9.0 中的新增功能，它由一组用类似于 Transact\-SQL 或 XQuery 的声明性语法所编写的子句组成。  不过，[!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] 公共语言运行库 \(CLR\) 无法读取查询表达式语法本身。  因此，在编译时，查询表达式将转换为 CLR 能理解的形式，即方法调用。  这些方法称为“标准查询运算符”。  作为开发人员，您可以选择使用方法语法而不使用查询语法直接调用这些方法。有关详细信息，请参阅[Query Syntax and Method Syntax in LINQ](../Topic/Query%20Syntax%20and%20Method%20Syntax%20in%20LINQ%20\(C%23\).md)。  
  
### 查询表达式语法  
 查询表达式是一种声明性查询语法。  通过这一语法，开发人员可以使用类似于 Transact\-SQL 的高级语言格式编写查询。  通过使用查询表达式语法，您可以用最少的代码对数据源执行复杂的筛选、排序和分组操作。  有关详细信息，请参阅[基本查询操作 \(Visual Basic\)](../Topic/Basic%20Query%20Operations%20\(Visual%20Basic\).md)。  有关演示如何使用查询表达式语法的示例，请参见以下主题：  
  
-   [查询表达式语法示例：投影](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-projection.md)  
  
-   [查询表达式语法示例：筛选](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-filtering.md)  
  
-   [查询表达式语法示例：排序](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-ordering.md)  
  
-   [查询表达式语法示例：聚合运算符](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-aggregate-operators.md)  
  
-   [查询表达式语法示例：分区](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-partitioning.md)  
  
-   [查询表达式语法示例：联接运算符](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-join-operators.md)  
  
-   [查询表达式语法示例：元素运算符](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-element-operators.md)  
  
-   [查询表达式语法示例：分组](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-grouping.md)  
  
-   [查询表达式语法示例：导航关系](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-navigating-relationships.md)  
  
### 基于方法的查询语法  
 另一种编写 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] 查询的方法是使用基于方法的查询。  基于方法的查询语法是一系列针对 LINQ 运算符方法的直接方法调用，同时将 lambda 表达式作为参数传递。  有关详细信息，请参阅 [Lambda 表达式](../Topic/Lambda%20Expressions%20\(C%23%20Programming%20Guide\).md)。  有关演示如何使用基于方法的语法的示例，请参见以下主题：  
  
-   [基于方法的查询语法示例：投影](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-projection.md)  
  
-   [基于方法的查询语法示例：筛选](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-filtering.md)  
  
-   [基于方法的查询语法示例：排序](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-ordering.md)  
  
-   [基于方法的查询语法示例：聚合运算符](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-aggregate-operators.md)  
  
-   [基于方法的查询语法示例：分区](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-partitioning.md)  
  
-   [基于方法的查询语法示例：转换](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-conversion.md)  
  
-   [基于方法的查询语法示例：联接运算符](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-join-operators.md)  
  
-   [基于方法的查询语法示例：元素运算符](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-element-operators.md)  
  
-   [基于方法的查询语法示例：分组](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-grouping.md)  
  
-   [基于方法的查询语法示例：导航关系](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-navigating-relationships.md)  
  
## 请参阅  
 [LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md)   
 [Getting Started with LINQ in C\#](../Topic/Getting%20Started%20with%20LINQ%20in%20C%23.md)   
 [Getting Started with LINQ in Visual Basic](../Topic/Getting%20Started%20with%20LINQ%20in%20Visual%20Basic.md)   
 [实体框架合并选项和已编译的查询](http://go.microsoft.com/fwlink/?LinkId=199591)