---
title: "值的比较 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "比较运算符, 比较表达式"
  - "表达式 [Visual Basic], 比较"
  - "数值表达式"
  - "运算符 [Visual Basic], 比较"
  - "变量 [Visual Basic], 比较值"
  - "Visual Basic 代码, 表达式"
  - "Visual Basic 代码, 运算符"
ms.assetid: 60da0c76-9458-4afc-97e9-44a7939c064c
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 值的比较 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

比较运算符可用于构造比较数值变量的值的表达式。  这些表达式根据比较结果为真还是假返回 `Boolean` 值。  此类表达式的示例如下所示。  
  
 `45 > 26`  
  
 `26 > 45`  
  
 第一个表达式的计算结果为 `True`，因为 45 大于 26。  第二个示例的计算结果为 `False`，因为 26 不大于 45。  
  
 也可以采用此形式比较数值表达式。  您比较的表达式本身可以是复杂表达式，如下面的示例所示。  
  
 `x / 45 * (y +17) >= System.Math.Sqrt(z) / (p - (x * 16))`  
  
 前面的复杂表达式包括文本、变量和函数调用。  计算比较运算符两侧的表达式，然后使用 `>=` 比较运算符比较结果值。  如果左侧表达式的值大于或等于右侧表达式的值，则整个表达式的计算结果为 `True`；否则，它的计算结果为 `False`。  
  
 比较值的表达式在 `If...Then` 构造中最常用，如下面的示例所示。  
  
 [!code-vb[VbVbalrOperators#84](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/value-comparisons_1.vb)]  
  
 `=` 符号是比较运算符，也是赋值运算符。  当用作比较运算符时，它计算左侧的值是否等于右侧的值，如下面的示例所示。  
  
 [!code-vb[VbVbalrOperators#85](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/value-comparisons_2.vb)]  
  
 也可在需要 `Boolean` 值的任意位置使用比较表达式，如在 `If`、`While`、`Loop` 或 `ElseIf` 语句中，或在将值赋予或传递给 `Boolean` 变量时使用。  在下面的示例中，比较表达式返回的值被赋给了 `Boolean` 变量。  
  
 [!code-vb[VbVbalrOperators#86](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/value-comparisons_3.vb)]  
  
## 请参阅  
 [布尔表达式](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)   
 [运算符和表达式](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [比较运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [如何：计算数值](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-calculate-numeric-values.md)   
 [Visual Basic 中的运算符优先级](../../../../visual-basic/language-reference/operators/operator-precedence.md)