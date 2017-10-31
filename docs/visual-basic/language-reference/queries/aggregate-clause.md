---
title: "Aggregate 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryAggregateIn"
  - "vb.QueryAggregate"
  - "vb.QueryAggregateInto"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Aggregate 子句"
  - "Aggregate 语句"
  - "查询 [Visual Basic], 聚合"
ms.assetid: 1315a814-5db6-4077-b34b-b141e11cc0eb
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# Aggregate 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对集合应用一个或多个聚合函数。  
  
## 语法  
  
```  
Aggregate element [As type] In collection _  
  [, element2 [As type2] In collection2, [...]]  
  [ clause ]  
  Into expressionList  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`element`|必选。  用于循环访问集合的元素的变量。|  
|`type`|可选。  `element` 的类型。  如果不指定类型，则从 `collection` 推断 `element` 的类型。|  
|`collection`|必选。  引用要对其进行操作的集合。|  
|`clause`|可选。  一个或多个查询子句（例如 `Where` 子句），用于优化要向其应用聚合子句的查询结果。|  
|`expressionList`|必选。  一个或多个由逗号分隔的表达式，标识要应用到集合的聚合函数。  可以对聚合函数应用一个别名，以便为查询结果指定成员名称。  如果不提供别名，则使用聚合函数的名称。  有关示例，请参见本主题后面有关聚合函数的部分。|  
  
## 备注  
 `Aggregate` 子句可用于在查询中包含聚合函数。  聚合函数对一组值执行检查和计算，并返回单个值。  使用查询结果类型的成员可以访问计算得到的值。  可以使用的标准聚合函数包括 `All`、`Any`、`Average`、`Count`、`LongCount`、`Max`、`Min` 和 `Sum` 函数。  这些函数对于熟悉 SQL 中聚合的开发人员而言并不陌生。  本主题的下一部分将介绍这些函数。  
  
 聚合函数的结果作为查询结果类型的字段包含在查询结果中。  可以为聚合函数结果提供别名，以指定将保存聚合值的查询结果类型成员的名称。  如果不提供别名，则使用聚合函数的名称。  
  
 `Aggregate` 子句可以开始查询，也可以作为附加子句包含在查询中。  如果 `Aggregate` 子句开始查询，则结果是单个值，该值是 `Into` 子句中指定的聚合函数的结果。  如果在 `Into` 子句中指定多个聚合函数，则查询会返回单个类型，而且，对于 `Into` 子句中的每个聚合函数，该类型都具有一个单独的属性，以引用该聚合函数的结果。  如果 `Aggregate` 子句作为附加子句包含在查询中，则对于 `Into` 子句中的每个聚合函数，查询集合中返回的类型都具有一个单独的属性，以引用该聚合函数的结果。  
  
## 聚合函数  
 下面的列表描述了可以在 `Aggregate` 子句中使用的标准聚合函数。  
  
|||  
|-|-|  
|功能|说明|  
|`All`|如果集合中的所有元素均满足指定条件，则返回 `true`；否则返回 `false`。  下面是一个示例：<br /><br /> [!code-vb[VbSimpleQuerySamples#5](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_1.vb)]|  
|`Any`|如果集合中的任一元素满足指定条件，则返回 `true`；否则返回 `false`。  下面是一个示例：<br /><br /> [!code-vb[VbSimpleQuerySamples#6](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_2.vb)]|  
|`Average`|计算集合中所有元素的平均值，或者对集合中的所有元素计算提供的表达式。  下面是一个示例：<br /><br /> [!code-vb[VbSimpleQuerySamples#7](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_3.vb)]|  
|`Count`|统计集合中的元素数量。  可以提供一个可选 `Boolean` 表达式，以便仅统计集合中满足条件的元素数量。  下面是一个示例：<br /><br /> [!code-vb[VbSimpleQuerySamples#8](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_4.vb)]|  
|`Group`|引用由 `Group By` 或 `Group Join` 子句进行分组的查询结果。  仅当 `Group` 函数位于 `Group By` 或 `Group Join` 子句的 `Into` 子句中时，该函数才有效。  有关更多信息和示例，请参见[Group By 子句](../../../visual-basic/language-reference/queries/group-by-clause.md)和[Group Join 子句](../../../visual-basic/language-reference/queries/group-join-clause.md)。|  
|`LongCount`|统计集合中的元素数量。  可以提供一个可选 `Boolean` 表达式，以便仅统计集合中满足条件的元素数量。  将结果作为 `Long` 类型的值返回。  有关示例，请参见 `Count` 聚合函数。|  
|`Max`|计算集合中的最大值，或对集合中的所有元素计算提供的表达式。  下面是一个示例：<br /><br /> [!code-vb[VbSimpleQuerySamples#9](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_5.vb)]|  
|`Min`|计算集合中的最小值，或对集合中的所有元素计算提供的表达式。  下面是一个示例：<br /><br /> [!code-vb[VbSimpleQuerySamples#10](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_6.vb)]|  
|`Sum`|计算集合中所有元素之和，或对集合中的所有元素计算提供的表达式。  下面是一个示例：<br /><br /> [!code-vb[VbSimpleQuerySamples#15](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_7.vb)]|  
  
## 示例  
 下面的代码示例演示如何使用 `Aggregate` 子句对查询结果应用聚合函数。  
  
 [!code-vb[VbSimpleQuerySamples#4](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_8.vb)]  
  
## 创建用户定义的聚合函数  
 可以通过将扩展方法添加到 <xref:System.Collections.Generic.IEnumerable%601> 类型，在查询表达式中包含您自己的自定义聚合函数。  然后，您的自定义方法可以对引用您的聚合函数的可枚举集合执行计算或操作。  有关扩展方法的更多信息，请参见[扩展方法](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)。  
  
 例如，下面的代码示例演示了一个自定义聚合函数，该函数计算一个数字集合的中值。  `Median` 扩展方法具有两个重载版本。  第一个重载接受 `IEnumerable(Of Double)` 类型集合作为输入。  如果对 `Double` 类型的查询字段调用 `Median` 聚合函数，则将调用此方法。  可以向 `Median` 方法的第二个重载传递任何泛型类型。  `Median` 方法的泛型重载接受另一个参数，该参数引用了 `Func(Of T, Double)` lambda 表达式，以便将集合中的类型的值投射为 `Double` 类型的相应值。  然后，它将中值的计算委托给 `Median` 方法的另一个重载。  有关 lambda 表达式的更多信息，请参见 [lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  
  
 [!code-vb[VbSimpleQuerySamples#18](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_9.vb)]  
  
 下面的代码示例演示了示例查询，这些查询对 `Integer` 类型集合和 `Double` 类型集合调用 `Median` 聚合函数。  对 `Double` 类型集合调用 `Median` 聚合函数的查询调用 `Median` 方法的接受 `Double` 类型集合作为输入的重载。  对 `Integer` 类型集合调用 `Median` 聚合函数的查询调用 `Median` 方法的泛型重载。  
  
 [!code-vb[VbSimpleQuerySamples#19](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_10.vb)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Where 子句](../../../visual-basic/language-reference/queries/where-clause.md)   
 [Group By 子句](../../../visual-basic/language-reference/queries/group-by-clause.md)