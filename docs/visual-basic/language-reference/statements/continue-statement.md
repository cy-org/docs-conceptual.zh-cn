---
title: "Continue 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.continue"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Continue 语句 [Visual Basic]"
  - "循环, 传递到下一个迭代"
ms.assetid: 3ad00103-358b-4af3-a3a8-1b9ea0e995d3
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# Continue 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

立即将控件传输到循环的下一个迭代。  
  
## 语法  
  
```  
Continue { Do | For | While }  
```  
  
## 备注  
 可以从 `Do`、 `For`或 `While` 循环内部调用到该循环的下一个迭代。  控件传递给循环条件立即进行测试，与调用等效于 `For` 或 `While` 语句，或向包含 `Until` 或 `While` 子句的 `Do` 或 `Loop` 语句。  
  
 可以在任意位置使用 `Continue` 在允许调用的循环。  允许控件转换的规则与 [GoTo 语句](../../../visual-basic/language-reference/statements/goto-statement.md)使用。  
  
 例如，因此，如果循环在 `Try` 中完全包含块， `Catch` 块，或者 `Finally` 块，可以使用 `Continue` 调用在循环之外。  如果为，则另一方面， `Try`…`End Try` 结构在循环内包含，则不能使用 `Continue` 到发送控件在 `Finally` 外部块，因此，您可以使用它调用 `Try` 外部或 `Catch` 块，才可以完全调用在 `Try`…`End Try` 结构之外。  
  
 如果嵌套循环的类型相同，例如在另一个 `Do` 循环中的一个 `Do` 循环， `Continue Do` 语句跳过到包含它最里层 `Do` 循环的下一个迭代。  不能使用 `Continue` 跳到同一类型的一个包含循环的下一次迭代。  
  
 如果嵌套不同类型的循环，使用 `Continue Do` 或 `Continue For`，如 `For` 循环，将中的一个 `Do` 循环可以跳到循环的下一个迭代。  
  
## 示例  
 ，如果除数为零，下面的代码示例使用 `Continue While` 语句跳过到数组中的下一列。  `Continue While` 是在 `For` 循环内。  传输到 `While col < lastcol` 语句，是最里层的 `While` 循环下一次迭代包含 `For` 循环。  
  
 [!code-vb[VbVbalrStatements#14](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/continue-statement_1.vb)]  
  
## 请参阅  
 [Do...Loop 语句](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [While...End While 语句](../../../visual-basic/language-reference/statements/while-end-while-statement.md)   
 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)