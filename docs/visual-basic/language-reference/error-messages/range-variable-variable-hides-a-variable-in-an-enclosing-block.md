---
title: "范围变量 &lt;变量&gt; 隐藏封闭块中的变量、以前定义的范围变量或在查询表达式中隐式声明的变量 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36633"
  - "vbc36633"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36633"
ms.assetid: 5d5470e4-3de5-49c2-8831-1087625f4a77
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# 范围变量 &lt;变量&gt; 隐藏封闭块中的变量、以前定义的范围变量或在查询表达式中隐式声明的变量
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在 `Select`、`From`、`Aggregate` 或 `Let` 子句中指定的范围变量名称与以前已在查询中指定的范围变量的名称或者由查询隐式声明的变量的名称（比如字段名或聚合函数的名称）完全相同。  
  
 **错误 ID：**BC36633  
  
### 更正此错误  
  
-   确保特定查询范围中的所有范围变量都具有唯一的名称。  可以将查询括在括号中以确保嵌套查询具有唯一的范围。  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Let 子句](../../../visual-basic/language-reference/queries/let-clause.md)   
 [Aggregate 子句](../../../visual-basic/language-reference/queries/aggregate-clause.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)