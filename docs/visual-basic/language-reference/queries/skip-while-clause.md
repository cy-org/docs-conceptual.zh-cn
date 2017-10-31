---
title: "Skip While 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QuerySkipWhile"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "查询 [Visual Basic], Skip While"
  - "Skip While 子句"
  - "Skip While 语句"
ms.assetid: 5dee8350-7520-4f1a-b00d-590cacd572d6
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Skip While 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

只要指定的条件为 `true`，就跳过集合中的元素，然后返回剩余的元素。  
  
## 语法  
  
```  
Skip While expression  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`expression`|必选。  表示元素测试条件的表达式。  该表达式必须返回 `Boolean` 值或功能上等效的值，例如计算结果为 `Boolean` 的 `Integer`。|  
  
## 备注  
 `Skip While` 子句从查询结果的开头跳过元素，直到提供的 `expression` 返回 `false` 为止。  在 `expression` 返回 `false` 后，查询返回所有剩余元素。  对于剩余结果，将忽略 `expression`。  
  
 `Skip While` 子句与 `Where` 子句的不同之处在于，`Where` 子句可用于将查询中所有不满足特定条件的元素都排除在外。  `Skip While` 子句仅在第一次不满足条件之前排除元素。  在处理经过排序的查询结果时，`Skip While` 子句最有用。  
  
 使用 `Skip` 子句，也可以从查询结果的开头跳过特定数目的结果。  
  
## 示例  
 下面的代码示例使用 `Skip While` 子句跳过第一个美国客户之前的结果。  
  
 [!code-vb[VbSimpleQuerySamples#3](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/skip-while-clause_1.vb)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Skip 子句](../../../visual-basic/language-reference/queries/skip-clause.md)   
 [Take While 子句](../../../visual-basic/language-reference/queries/take-while-clause.md)   
 [Where 子句](../../../visual-basic/language-reference/queries/where-clause.md)