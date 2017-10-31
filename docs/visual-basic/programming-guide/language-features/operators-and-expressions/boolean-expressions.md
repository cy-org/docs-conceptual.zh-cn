---
title: "布尔表达式 (Visual Basic) | Microsoft Docs"
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
  - "Boolean 表达式"
  - "表达式计算, Boolean 表达式"
  - "表达式 [Visual Basic], Boolean"
  - "逻辑运算符, Boolean 表达式"
  - "逻辑运算符, 短路处理"
  - "运算符 [Visual Basic], Boolean"
  - "运算符 [Visual Basic], 短路处理"
  - "短路计算"
  - "短路处理"
  - "Visual Basic 代码, 表达式"
  - "Visual Basic 代码, 运算符"
ms.assetid: d3d90406-55c8-4404-8143-50fd7f0d0d1a
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 布尔表达式 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

“Boolean 表达式”是一种表达式，它计算 [Boolean 数据类型](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)的值：`True` 或 `False`。  `Boolean` 表达式可以有多种形式。  最简单的形式是将 `Boolean` 变量的值与 `Boolean` 文本直接比较，如下面的示例所示：  
  
 [!code-vb[VbVbalrOperators#87](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/boolean-expressions_1.vb)]  
  
## \= 运算符的两种含义  
 请注意，赋值语句 `newCustomer = True` 看起来与前面示例中的表达式一样，但它执行不同的功能，而且用法也不同。  在前面的示例中，表达式 `newCustomer = True` 表示 Boolean 值，因此 `=` 符号被解释为比较运算符。  在独立语句中，`=` 被解释为赋值运算符，并将右侧的值赋给左侧的变量。  下面的示例阐释了这一点。  
  
 [!code-vb[VbVbalrOperators#88](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/boolean-expressions_2.vb)]  
  
 有关进一步信息，请参见 [值的比较](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md) 和 [语句](../../../../visual-basic/language-reference/statements/index.md)。  
  
## 比较运算符  
 诸如 `=`、`<`、`>`、`<>`、`<=` 和 `>=` 等比较运算符通过将运算符左侧的表达式与运算符右侧的表达式进行比较，并将结果计算为 `True` 或 `False`，从而生成 Boolean 表达式。  下面的示例阐释了这一点。  
  
 `42 < 81`  
  
 由于 42 小于 81，因此前面示例中的 Boolean 表达式的计算结果为 `True`。  有关这种表达式的更多信息，请参见 [值的比较](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)。  
  
### 使用逻辑运算符组合的比较运算符  
 可以使用逻辑运算符组合比较表达式，以产生更复杂的 Boolean 表达式。  下面的示例演示结合使用比较运算符和逻辑运算符的情况：  
  
 `x > y And x < 1000`  
  
 在前面的示例中，整个表达式的值取决于 `And` 运算符两侧表达式的值。  如果两个表达式都为 `True`，则整个表达式的计算结果为 `True`。  如果任何一个表达式为 `False`，则整个表达式的计算结果为 `False`。  
  
## 短路运算符  
 逻辑运算符 `AndAlso` 和 `OrElse` 表现称为“短路”的行为。  短路运算符首先计算左侧操作数。  如果左侧操作数确定整个表达式的值，则程序执行过程将在不计算右侧表达式的情况下继续。  下面的示例阐释了这一点。  
  
 [!code-vb[VbVbalrOperators#89](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/boolean-expressions_3.vb)]  
  
 在前面的示例中，运算符将计算左侧的表达式 `45 < 12`。  由于左侧表达式的计算结果为 `False`，因此，整个逻辑表达式的计算结果必须为 `False`。  程序执行过程因此跳过执行 `If` 块内的代码，而不计算右侧表达式 `testFunction(3)`。  此示例不调用 `testFunction()`，因为左侧表达式证明整个表达式为假。  
  
 同样，如果使用 `OrElse` 的逻辑表达式中的左侧表达式计算结果为 `True`，则执行过程继续下一行代码，而不计算右侧表达式，因为左侧表达式已经证明整个表达式为真。  
  
### 使用非短路运算符进行比较  
 相反，当使用逻辑运算符 `And` 和 `Or` 时，逻辑运算符的两侧都要计算。  下面的示例阐释了这一点。  
  
 [!code-vb[VbVbalrOperators#90](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/boolean-expressions_4.vb)]  
  
 前面的示例将调用 `testFunction()`，即使左侧表达式的计算结果为 `False`。  
  
## 加括号的表达式  
 可以使用括号控制 Boolean 表达式的求值顺序。  放在括号中的表达式首先计算。  对于多层嵌套，嵌套最深的表达式最优先。  在括号内，计算过程按照运算符优先级的规则进行。  有关更多信息，请参见 [Visual Basic 中的运算符优先级](../../../../visual-basic/language-reference/operators/operator-precedence.md)。  
  
## 请参阅  
 [Visual Basic 中的逻辑运算符和位运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)   
 [值的比较](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [语句](../../../../visual-basic/programming-guide/language-features/statements.md)   
 [比较运算符](../../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [运算符的有效组合](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)   
 [Visual Basic 中的运算符优先级](../../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Boolean 数据类型](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)