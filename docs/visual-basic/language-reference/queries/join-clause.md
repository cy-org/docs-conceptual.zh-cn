---
title: "Join 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryJoinIn"
  - "vb.QueryJoin"
  - "vb.QueryJoinOn"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Join 子句"
  - "Join 语句"
  - "查询 [Visual Basic], 联接"
ms.assetid: 6dd37936-b27c-4e00-98ad-154b23f4de64
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Join 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将两个集合组合为单个集合。  联接操作基于匹配键，使用 `Equals` 运算符。  
  
## 语法  
  
```  
Join element In collection _  
  [ joinClause _ ]   
  [ groupJoinClause ... _ ]   
On key1 Equals key2 [ And key3 Equals key4 [... ]  
```  
  
## 部件  
 `element`  
 必需。  要联接的集合的控制变量。  
  
 `collection`  
 必需。  要与 `Join` 运算符左侧的集合组合的集合。  `Join` 子句可以嵌套在另一个 `Join` 子句中，也可以嵌套在 `Group Join` 子句中。  
  
 `joinClause`  
 可选。  用于进一步限制查询的一个或多个其他 `Join` 子句。  
  
 `groupJoinClause`  
 可选。  用于进一步限制查询的一个或多个其他 `Group Join` 子句。  
  
 `key1` `Equals` `key2`  
 必需。  标识要联接的集合的键。  必须使用 `Equals` 运算符来比较要联接的集合的键。  您可以使用 `And` 运算符标识多个键，从而组合联接条件。  `key1` 必须来自于 `Join` 运算符左侧的集合。  `key2` 必须来自于 `Join` 运算符右侧的集合。  
  
 在联接条件中使用的键可以是包含集合中的多个项的表达式。  不过，每个键表达式只能包含其各自集合中的项。  
  
## 备注  
 `Join` 子句基于要联接的集合中的匹配键值组合两个集合。  所得集合可以包含 `Join` 运算符左侧标识的集合和 `Join` 子句中标识的集合的值的任何组合。  查询将只返回满足 `Equals` 运算符所指定的条件的结果。  这等效于 SQL 中的 `INNER JOIN`。  
  
 可以在查询中使用多个 `Join` 子句，以便将两个或更多集合联接为单个集合。  
  
 在不使用 `Join` 子句的情况下，可以执行隐式联接来组合集合。  为此，应在 `From` 子句中包括多个 `In` 子句，并指定标识要用于联接的键的 `Where` 子句。  
  
 使用 `Group Join` 子句可以将多个集合组合为单个分层集合。  这与 SQL 中的 `LEFT OUTER JOIN` 类似。  
  
## 示例  
 下面的代码示例执行隐式联接将客户列表与其订单组合在一起。  
  
 [!code-vb[VbSimpleQuerySamples#13](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/join-clause_1.vb)]  
  
## 示例  
 下面的代码示例使用 `Join` 子句联接两个集合。  
  
 [!code-vb[VbSimpleQuerySamples#12](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/join-clause_2.vb)]  
  
 此示例将生成类似下面的输出：  
  
 `winlogon (968), Windows Logon`  
  
 `explorer (2424), File Explorer`  
  
 `cmd (5136), Command Window`  
  
## 示例  
 下面的代码示例通过使用包含两个键列的 `Join` 子句来联接两个集合。  
  
 [!code-vb[VbSimpleQuerySamples#17](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/join-clause_3.vb)]  
  
 此示例将生成类似下面的输出：  
  
 `winlogon (968), Windows Logon, Priority = 13`  
  
 `cmd (700), Command Window, Priority = 8`  
  
 `explorer (2424), File Explorer, Priority = 8`  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [查询](../../../visual-basic/language-reference/queries/queries.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Group Join 子句](../../../visual-basic/language-reference/queries/group-join-clause.md)   
 [Where 子句](../../../visual-basic/language-reference/queries/where-clause.md)