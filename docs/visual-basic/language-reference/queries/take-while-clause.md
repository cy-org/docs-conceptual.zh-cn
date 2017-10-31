---
title: "Take While 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryTakeWhile"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "查询 [Visual Basic], Take While"
  - "Take While 子句"
  - "Take While 语句"
ms.assetid: db8f9f2f-fc9f-4a6c-b0b8-1bf048147e11
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Take While 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

只要指定的条件为 `true`，就包含集合中相应的元素，并跳过剩余的元素。  
  
## 语法  
  
```  
Take While expression  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`expression`|必选。  表示元素测试条件的表达式。  该表达式必须返回 `Boolean` 值或功能上等效的值，例如计算结果为 `Boolean` 的 `Integer`。|  
  
## 备注  
 `Take While` 子句从查询结果的开头包含元素，直到提供的 `expression` 返回 `false` 为止。  在 `expression` 返回 `false` 后，查询会跳过所有剩余元素。  对于剩余结果，将忽略 `expression`。  
  
 `Take While` 子句与 `Where` 子句的不同之处在于，`Where` 子句可以用于包含查询中所有满足特定条件的元素。  `Take While` 子句仅包含第一次不满足条件之前的元素。  在处理经过排序的查询结果时，`Take While` 子句最有用。  
  
## 示例  
 下面的代码示例使用 `Take While` 子句检索结果，直到找到第一个没有任何订单的客户为止。  
  
 [!code-vb[VbSimpleQuerySamples#2](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/take-while-clause_1.vb)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Take 子句](../../../visual-basic/language-reference/queries/take-clause.md)   
 [Skip While 子句](../../../visual-basic/language-reference/queries/skip-while-clause.md)   
 [Where 子句](../../../visual-basic/language-reference/queries/where-clause.md)