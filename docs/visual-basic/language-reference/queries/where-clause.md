---
title: "Where 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryWhere"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "查询 [Visual Basic], Where"
  - "Where 子句"
  - "Where 语句"
ms.assetid: 48b5c2c5-3181-429c-8545-894296798c89
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Where 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定查询的筛选条件。  
  
## 语法  
  
```  
Where condition  
```  
  
## 部件  
 `condition`  
 必选。  一个表达式，确定是否在输出集合中包含集合中当前项的值。  该表达式的计算结果必须为 `Boolean` 值或 `Boolean` 值的等效值。  如果条件的计算结果为 `True`，则在查询结果中包含该元素；否则从查询结果中排除该元素。  
  
## 备注  
 使用 `Where` 子句，可以通过仅选择满足特定条件的元素来筛选查询数据。  其值使 `Where` 子句的计算结果为 `True` 的元素将包含在查询结果中；其他元素将被排除。  `Where` 子句中使用的表达式的计算结果必须为 `Boolean` 值或 `Boolean` 值的等效值（例如 Integer 值 — 当其值为 0 时，计算结果为 `False`）。  使用逻辑运算符（如 `And`、`Or`、`AndAlso`、`OrElse`、`Is` 和 `IsNot`）可以将多个表达式组合在一个 `Where` 子句中。  
  
 默认情况下，查询表达式直到被访问时（例如，当它们进行数据绑定或在 `For` 循环中进行循环访问时）才计算结果。  因此，在访问查询前，不会计算 `Where` 子句。  如果值位于 `Where` 子句中使用的查询外部，请确保查询执行时在 `Where` 子句中使用适当的值。  有关查询执行的更多信息，请参见[编写第一个 LINQ 查询](../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md)。  
  
 您可以在 `Where` 子句中调用函数，以便对集合中当前元素的值执行计算或运算。  在 `Where` 子句中调用函数可使查询在定义后立即执行，而不是在访问时执行。  有关查询执行的更多信息，请参见[编写第一个 LINQ 查询](../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md)。  
  
## 示例  
 下面的查询表达式使用 `From` 子句为 `customers` 集合中的每个 `Customer` 对象声明范围变量 `cust`。  `Where` 子句使用范围变量将输出限制为指定地区的客户。  `For Each` 循环在查询结果中显示每个客户的公司名称。  
  
 [!code-vb[VbSimpleQuerySamples#23](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/where-clause_1.vb)]  
  
## 示例  
 下面的示例在 `Where` 子句使用 `And` 和 `Or` 逻辑运算符。  
  
 [!code-vb[VbSimpleQuerySamples#31](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/where-clause_2.vb)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [For Each...Next 语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)