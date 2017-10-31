---
title: "Group Join 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryGroupJoinIn"
  - "vb.QueryGroupJoinOn"
  - "vb.QueryGroupJoin"
  - "vb.QueryGroupJoinInto"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Group Join 子句"
  - "Group Join 语句"
  - "查询 [Visual Basic], Group Join"
ms.assetid: 37dbf79c-7b5c-421b-bbb7-dadfd2b92a1c
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# Group Join 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将两个集合组合为单个分层集合。  联接运算基于匹配的键。  
  
## 语法  
  
```  
Group Join element [As type] In collection _  
  On key1 Equals key2 [ And key3 Equals key4 [... ] ] _  
  Into expressionList  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`element`|必选。  要联接的集合的控制变量。|  
|`type`|可选。  `element` 的类型。  如果不指定 `type`，则从 `collection` 推断 `element` 的类型。|  
|`collection`|必选。  要与 `Group Join` 运算符左侧的集合组合的集合。  `Group Join` 子句可以嵌套在 `Join` 子句或另一个 `Group Join` 子句中。|  
|`key1` `Equals` `key2`|必选。  标识要联接的集合的键。  必须使用 `Equals` 运算符来比较要联接的集合的键。  您可以使用 `And` 运算符标识多个键，从而组合联接条件。  `key1` 参数必须来自于 `Join` 运算符左侧的集合。  `key2` 参数必须来自于 `Join` 运算符右侧的集合。<br /><br /> 在联接条件中使用的键可以是包含集合中的多个项的表达式。  不过，每个键表达式只能包含其各自集合中的项。|  
|`expressionList`|必选。  一个或多个表达式，标识对集合中的元素组进行聚合的方式。  若要为分组结果标识一个成员名称，可使用 `Group` 关键字 \(`<alias> = Group`\)。  还可以包含要应用于组的聚合函数。|  
  
## 备注  
 `Group Join` 子句基于要联接的集合中的匹配键值组合两个集合。  产生的集合可以包含一个如下所述的成员：该成员引用由第二个集合中的元素组成的集合，这些元素与第一个集合中的键值相匹配。  您还可以指定要应用到第二个集合中的分组元素的聚合函数。  有关聚合函数的信息，请参见 [Aggregate 子句](../../../visual-basic/language-reference/queries/aggregate-clause.md)。  
  
 例如，请考虑一个经理集合和一个雇员集合。  这两个集合的元素都具有一个 ManagerID 属性，用于标识向特定经理汇报的雇员。  联接运算的结果将包含具有匹配 ManagerID 值的每个经理和雇员所对应的结果。  `Group Join` 运算的结果将包含完整的经理列表。  每个经理结果都将包含一个成员，该成员引用与特定经理匹配的雇员的列表。  
  
 `Group Join` 运算产生的集合可以包含来自 `From` 子句中标识的集合以及 `Group Join` 子句的 `Into` 子句中标识的表达式的值的任意组合。  有关 `Into` 子句的有效表达式的更多信息，请参见 [Aggregate 子句](../../../visual-basic/language-reference/queries/aggregate-clause.md)。  
  
 `Group Join` 运算将返回 `Group Join` 运算符左侧标识的集合中的所有结果。  即使要联接的集合中没有匹配项，也是如此。  这与 SQL 中的 `LEFT OUTER JOIN` 类似。  
  
 可以使用 `Join` 子句将两个集合组合为单个集合。  这等效于 SQL 中的 `INNER JOIN`。  
  
## 示例  
 下面的代码示例使用 `Group Join` 子句联接两个集合。  
  
 [!code-vb[VbSimpleQuerySamples#14](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/group-join-clause_1.vb)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Join 子句](../../../visual-basic/language-reference/queries/join-clause.md)   
 [Where 子句](../../../visual-basic/language-reference/queries/where-clause.md)   
 [Group By 子句](../../../visual-basic/language-reference/queries/group-by-clause.md)