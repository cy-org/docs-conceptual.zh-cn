---
title: "Take 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryTake"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "查询 [Visual Basic], Take"
  - "Take 子句"
  - "Take 语句"
ms.assetid: 77bf87b2-1476-4456-957f-fee922fbad8c
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Take 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

从集合开始处起，返回指定数量的连续元素。  
  
## 语法  
  
```  
Take count  
```  
  
## 部件  
 `count`  
 必选。  一个值或一个表达式，等于要返回的序列的元素个数。  
  
## 备注  
 如果使用 `Take` 子句，则查询包括从结果列表开始处起的指定数量的连续元素。  要包括的元素个数是由 `count` 参数指定的。  
  
 同时使用 `Take` 子句和 `Skip` 子句可以从查询的任何位置起返回一定范围的数据。  为此，请该范围的第一个元素的索引传递给 `Skip` 子句，将该范围的大小传递给 `Take` 子句。  这种情况下，必须在 `Skip` 子句之后指定 `Take` 子句。  
  
 如果在查询中使用 `Take` 子句，还需要确保按顺序返回结果，这样 `Take` 子句才能包括预期的结果。  有关对查询结果进行排序的更多信息，请参见 [Order By 子句](../../../visual-basic/language-reference/queries/order-by-clause.md)。  
  
 使用 `TakeWhile` 子句可以指定，根据提供的条件仅返回某些元素。  
  
## 示例  
 下面的代码示例同时使用 `Take` 子句和 `Skip` 子句在页面中返回查询数据。  GetCustomers 函数使用 `Skip` 子句跳过列表中的客户，直至到达提供的起始索引值为止，并使用 `Take` 子句返回从该索引值开始的客户页。  
  
 [!code-vb[VbSimpleQuerySamples#1](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/take-clause_1.vb)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Order By 子句](../../../visual-basic/language-reference/queries/order-by-clause.md)   
 [Take While 子句](../../../visual-basic/language-reference/queries/take-while-clause.md)   
 [Skip 子句](../../../visual-basic/language-reference/queries/skip-clause.md)