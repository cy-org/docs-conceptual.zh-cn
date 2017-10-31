---
title: "Let 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryLet"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Let 子句"
  - "Let 语句"
  - "查询 [Visual Basic], Let"
ms.assetid: 981aa516-16eb-4c53-b1f1-5aa3e82f316e
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Let 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

计算一个值并将该值赋给查询中的新变量。  
  
## 语法  
  
```  
Let variable = expression [, ...]  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`variable`|必选。  一个别名，可用于引用所提供的表达式的结果。|  
|`expression`|必选。  一个将进行计算并赋值给指定变量的表达式。|  
  
## 备注  
 在 `Let` 子句中，可以计算每个查询结果的值，可以通过别名引用这些值。  别名可以在其他子句（如 `Where` 子句）中使用。  在 `Let` 子句中，可以创建可读性更强的查询语句，这是因为可以为查询所包含的表达式子句指定别名，在每次使用该表达式子句时，都可以用该别名替代。  
  
 在 `Let` 子句中，可以对任意数量的 `variable` 和 `expression` 赋值。  用逗号 \(,\) 分隔每个赋值语句。  
  
## 示例  
 下面的代码示例使用 `Let` 子句计算产品 10% 的折扣。  
  
 [!code-vb[VbSimpleQuerySamples#16](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/let-clause_1.vb)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Where 子句](../../../visual-basic/language-reference/queries/where-clause.md)