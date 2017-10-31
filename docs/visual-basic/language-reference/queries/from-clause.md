---
title: "From 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryFrom"
  - "vb.QueryFromIn"
  - "vb.QueryFromLet"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "From 子句"
  - "From 语句"
  - "查询 [Visual Basic], From"
ms.assetid: 83e3665e-68a0-4540-a3a3-3d777a0f95d5
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# From 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定要查询的一个或多个范围变量和一个集合。  
  
## 语法  
  
```  
From element [ As type ] In collection [ _ ]  
  [, element2 [ As type2 ] In collection2 [, ... ] ]  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`element`|必选。  一个范围变量，用于循环访问集合的元素。  一个范围变量，用于在查询循环访问 `collection` 时，引用 `collection` 的每个成员。  必须为可枚举类型。|  
|`type`|可选。  `element` 的类型。  如果不指定 `type`，则从 `collection` 推断 `element` 的类型。|  
|`collection`|必选。  引用要查询的集合。  必须为可枚举类型。|  
  
## 备注  
 `From` 子句用于标识查询的源数据，以及用于引用源集合中元素的变量。  这些变量称为范围变量。  查询必须使用 `From` 子句，除非使用 `Aggregate` 子句来标识仅返回聚合结果的查询。  有关更多信息，请参见 [Aggregate 子句](../../../visual-basic/language-reference/queries/aggregate-clause.md)。  
  
 可以指定查询中的多个 `From` 子句，以标识要联接的多个集合。  指定多个集合时，将单独循环访问这些集合，或者如果这些集合是相关的，则可以联接它们。  您可以通过使用 `Select` 子句隐式联接集合，或者通过使用 `Join` 或 `Group Join` 子句显式联接集合。  或者，您可以在单个 `From` 子句中指定多个范围变量和集合，并用逗号将每个相关的范围变量和集合分隔开。  下面的代码示例演示 `From` 子句的两个语法选项。  
  
 [!code-vb[VbSimpleQuerySamples#21](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/from-clause_1.vb)]  
  
 `From` 子句定义查询的范围，类似于 `For` 循环的范围。  因此，查询范围中的每个 `element` 范围变量必须具有唯一名称。  因为您可以为查询指定多个 `From` 子句，所以后续 `From` 子句可以引用 `From` 子句中的范围变量，或者它们可以引用以前的 `From` 子句中的范围变量。  例如，下面的示例演示一个嵌套 `From` 子句，其中第二个子句中的集合基于第一个子句中的范围变量的属性。  
  
 [!code-vb[VbSimpleQuerySamples#22](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/from-clause_2.vb)]  
  
 每个 `From` 子句后面可跟其他查询子句的任意组合以优化查询。  可以通过以下方式优化查询：  
  
-   通过使用 `From` 和 `Select` 子句隐式组合多个集合，或者使用 `Join` 或 `Group Join` 子句显式组合多个集合。  
  
-   使用 `Where` 子句筛选查询结果。  
  
-   使用 `Order By` 语句对结果进行排序。  
  
-   使用 `Group By` 子句对类似结果进行分组。  
  
-   使用 `Aggregate` 子句标识聚合函数，以对整个查询结果进行计算。  
  
-   使用 `Let` 子句引入迭代变量，该变量的值由表达式而不是集合决定。  
  
-   使用 `Distinct` 子句忽略重复查询结果。  
  
-   使用 `Skip`、`Take`、`Skip While` 和 `Take While` 子句，标识要返回的结果的各个部分。  
  
## 示例  
 下面的查询表达式使用 `From` 子句为 `customers` 集合中的每个 `Customer` 对象声明范围变量 `cust`。  `Where` 子句使用范围变量将输出限制为指定地区的客户。  `For Each` 循环在查询结果中显示每个客户的公司名称。  
  
 [!code-vb[VbSimpleQuerySamples#23](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/from-clause_3.vb)]  
  
## 请参阅  
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [For Each...Next 语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [Where 子句](../../../visual-basic/language-reference/queries/where-clause.md)   
 [Aggregate 子句](../../../visual-basic/language-reference/queries/aggregate-clause.md)   
 [Distinct 子句](../../../visual-basic/language-reference/queries/distinct-clause.md)   
 [Join 子句](../../../visual-basic/language-reference/queries/join-clause.md)   
 [Group Join 子句](../../../visual-basic/language-reference/queries/group-join-clause.md)   
 [Order By 子句](../../../visual-basic/language-reference/queries/order-by-clause.md)   
 [Let 子句](../../../visual-basic/language-reference/queries/let-clause.md)   
 [Skip 子句](../../../visual-basic/language-reference/queries/skip-clause.md)   
 [Take 子句](../../../visual-basic/language-reference/queries/take-clause.md)   
 [Skip While 子句](../../../visual-basic/language-reference/queries/skip-while-clause.md)   
 [Take While 子句](../../../visual-basic/language-reference/queries/take-while-clause.md)