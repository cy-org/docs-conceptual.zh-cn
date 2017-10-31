---
title: "Skip 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QuerySkip"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "查询 [Visual Basic], Skip"
  - "Skip 子句"
  - "Skip 语句"
ms.assetid: f00eb172-3907-4c43-9745-d8546ab86234
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Skip 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

跳过集合中指定数量的元素，然后返回剩余的元素。  
  
## 语法  
  
```  
Skip count  
```  
  
## 部件  
 `count`  
 必选。  一个值或一个表达式，其计算结果为要跳过的序列中的元素个数。  
  
## 备注  
 `Skip` 子句使查询跳过结果列表开头的元素并返回剩余的元素。  要跳过的元素个数由 `count` 参数标识。  
  
 可以将 `Skip` 子句与 `Take` 子句一起使用，以便从查询的任何段返回某一范围的数据。  为此，请该范围的第一个元素的索引传递给 `Skip` 子句，将该范围的大小传递给 `Take` 子句。  
  
 在查询中使用 `Skip` 子句时，可能还需要确保按照顺序返回结果，以使 `Skip` 子句能够跳过预期的结果。  有关对查询结果进行排序的更多信息，请参见 [Order By 子句](../../../visual-basic/language-reference/queries/order-by-clause.md)。  
  
 使用 `SkipWhile` 子句可以指定只根据提供的条件忽略特定元素。  
  
## 示例  
 下面的代码示例将 `Skip` 子句与 `Take` 子句一起使用，以便从页查询中返回数据。  `GetCustomers` 函数使用 `Skip` 子句跳过列表中的客户，直至到达提供的起始索引值为止，并使用 `Take` 子句返回从该索引值开始的客户页。  
  
 [!code-vb[VbSimpleQuerySamples#1](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/skip-clause_1.vb)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Order By 子句](../../../visual-basic/language-reference/queries/order-by-clause.md)   
 [Skip While 子句](../../../visual-basic/language-reference/queries/skip-while-clause.md)   
 [Take 子句](../../../visual-basic/language-reference/queries/take-clause.md)