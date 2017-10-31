---
title: "Distinct 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryDistinct"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Distinct 子句"
  - "Distinct 语句"
  - "查询 [Visual Basic], Distinct"
ms.assetid: 86f42614-0d8f-4ffc-b888-ce8a37a8d36a
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Distinct 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

限制当前范围变量的值，以消除后续查询子句中的重复值。  
  
## 语法  
  
```  
Distinct  
```  
  
## 备注  
 使用 `Distinct` 子句可以返回唯一项的列表。  使用 `Distinct` 子句将使查询忽略重复查询结果。  `Distinct` 子句应用于 `Select` 子句指定的所有返回字段的重复值。  如果没有指定 `Select` 子句，则 `Distinct` 子句应用于在 `From` 子句中标识的查询的范围变量。  如果范围变量不是不可变类型，则查询只有在类型的所有成员都与现有查询结果匹配时，才会忽略查询结果。  
  
## 示例  
 下面的查询表达式联接一个客户列表和一个客户订单列表。  包含 `Distinct` 子句，以返回唯一客户姓名和订单日期的列表。  
  
 [!code-vb[VbSimpleQuerySamples#20](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/distinct-clause_1.vb)]  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [Where 子句](../../../visual-basic/language-reference/queries/where-clause.md)