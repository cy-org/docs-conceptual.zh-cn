---
title: "Visual Basic 中的逻辑运算符和位运算符 | Microsoft Docs"
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
  - "And 运算符 [Visual Basic], 逻辑运算符"
  - "AndAlso 运算符"
  - "Boolean 表达式"
  - "表达式 [Visual Basic], Boolean"
  - "逻辑运算符"
  - "逻辑运算符, binary"
  - "逻辑运算符, Boolean 表达式"
  - "逻辑运算符, 短路处理"
  - "逻辑运算符, 一元的"
  - "Not 运算符 [Visual Basic], Boolean 表达式"
  - "运算符 [Visual Basic], 逻辑"
  - "Or 运算符, 逻辑运算符"
  - "OrElse 运算符 [Visual Basic]"
  - "短路处理"
  - "短路处理, 逻辑运算符"
  - "Visual Basic 代码, 表达式"
  - "Visual Basic 代码, 运算符"
  - "异或运算符 [Visual Basic], Boolean 表达式"
ms.assetid: ca474e13-567d-4b1d-a18b-301433705e57
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Visual Basic 中的逻辑运算符和位运算符
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

逻辑运算符比较 `Boolean` 表达式，并返回 `Boolean` 结果。  `And`、`Or`、`AndAlso`、`OrElse` 和 `Xor` 运算符是二元运算符，原因是它们接受两个操作数，而 `Not` 运算符是一元运算符，原因是它只接受一个操作数。  上述的某些运算符也可对整数值执行按位逻辑运算。  
  
## 一元逻辑运算符  
 [Not 运算符](../../../../visual-basic/language-reference/operators/not-operator.md) 对 `Boolean` 表达式执行逻辑求反。  它生成其操作数的逻辑相反值。  如果表达式的计算结果为 `True`，则 `Not` 返回 `False`；如果表达式的计算结果为 `False`，则 `Not` 返回 `True`。  下面的示例阐释了这一点。  
  
 [!code-vb[VbVbalrOperators#77](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/logical-and-bitwise-operators_1.vb)]  
  
## 二元逻辑运算符  
 [And 运算符](../../../../visual-basic/language-reference/operators/and-operator.md) 对两个 `Boolean` 表达式执行逻辑合取。  如果两个表达式的计算结果均为 `True`，则 `And` 返回 `True`。  如果其中至少一个表达式的计算结果为 `False`，则 `And` 返回 `False`。  
  
 [Or 运算符](../../../../visual-basic/language-reference/operators/or-operator.md) 对两个 `Boolean` 表达式执行逻辑析取或包含。  如果任意一个表达式的计算结果为 `True`，或两个表达式的计算结果均为 `True`，则 `Or` 返回 `True`。  如果两个表达式的计算结果都不是 `True`，则 `Or` 返回 `False`。  
  
 [异或运算符](../../../../visual-basic/language-reference/operators/xor-operator.md) 对两个 `Boolean` 表达式执行逻辑互斥。  如果恰好只有一个表达式的计算结果为 `True`（而不是两个都是），`Xor` 返回 `True`。  如果两个表达式的计算结果都是 `True`，或两者的计算结果都是 `False`，`Xor` 将返回 `False`。  
  
 下面的示例演示了 `And`、`Or` 和 `Xor` 运算符。  
  
 [!code-vb[VbVbalrOperators#78](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/logical-and-bitwise-operators_2.vb)]  
  
## 短路逻辑运算  
 [AndAlso 运算符](../../../../visual-basic/language-reference/operators/andalso-operator.md) 与 `And` 运算符非常类似，因为它也对两个 `Boolean` 表达式执行逻辑合取。  两者之间的主要差异是 `AndAlso` 表现出短路行为。  如果 `AndAlso` 表达式中第一个表达式的计算结果为 `False`，则不会计算第二个表达式的值，因为它不会改变最终结果，`AndAlso` 将返回 `False`。  
  
 同样，[OrElse 运算符](../../../../visual-basic/language-reference/operators/orelse-operator.md) 对两个 `Boolean` 表达式执行短路逻辑或。  如果 `OrElse` 表达式中第一个表达式的计算结果为 `True`，则不会计算第二个表达式的值，因为它不会改变最终结果，`OrElse` 将返回 `True`。  
  
### 短路平衡  
 通过不计算无法改变逻辑运算结果的表达式，短路可以提高性能。  但是，如果该表达式执行附加操作，短路将会跳过这些操作。  例如，如果表达式包括对 `Function` 过程的调用，那么，如果表达式已短路，则不会调用该过程，并且 `Function` 中包含的任何附加代码都不会运行。  因此，该功能可能只会偶尔运行，并且可能无法正确测试它。  或者，程序逻辑可能取决于`Function`中的代码。  
  
 下面的示例演示了 `And`、`Or` 与其短路副本之间的差异。  
  
 [!code-vb[VbVbalrOperators#81](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/logical-and-bitwise-operators_3.vb)]  
  
 [!code-vb[VbVbalrOperators#80](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/logical-and-bitwise-operators_4.vb)]  
  
 [!code-vb[VbVbalrOperators#79](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/logical-and-bitwise-operators_5.vb)]  
  
 在前面的示例中，请注意，在调用短路时，`checkIfValid()` 内部的某些重要代码将不会运行。  即使 `12 > 45` 返回 `False`，第一个 `If` 语句也会调用 `checkIfValid()`，因为 `And` 不会短路。  第二个 `If` 语句不会调用 `checkIfValid()`，因为当 `12 > 45` 返回 `False` 时，`AndAlso` 将会使第二个表达式短路。  即使 `12 < 45` 返回 `True`，第三个 `If` 语句也会调用 `checkIfValid()`，因为 `Or` 不会短路。  第四个 `If` 语句不会调用 `checkIfValid()`，因为当 `12 < 45` 返回 `True` 时，`OrElse` 将会使第二个表达式短路。  
  
## 按位运算  
 按位运算采用二进制（以 2 为基）形式计算两个整数值。  它们比较对应位置上的位，然后基于比较的结果赋值。  下面的示例演示了 `And` 运算符。  
  
 [!code-vb[VbVbalrConcepts#2](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/codesnippet/VisualBasic/logical-and-bitwise-operators_6.vb)]  
  
 前面的示例将 `x` 的值设置为 1。  发生这种情况的原因如下：  
  
-   这些值以二进制形式处理：  
  
     二进制格式的 3 为 011  
  
     二进制格式的 5 为 101  
  
-   `And` 运算符比较这些二进制表示方式，一次比较一个二进制位置（位）。  如果给定位置的两个位都为 1，则将 1 放在结果中的该位置。  如果任何一个位是 0，则将 0 放在结果中的该位置。  在前面的示例中，按如下所示计算结果：  
  
     011（二进制格式的 3）  
  
     101（二进制格式的 5）  
  
     001（二进制格式的计算结果）  
  
-   计算结果以十进制形式处理。  值 001 是 1 的二进制表示形式，因此 `x` \= 1。  
  
 除了在任何一个比较位是 1 或两个比较位都是 1 的情况下将 1 赋予结果位以外，按位 `Or` 运算与此类似。  `Xor` 在比较的位正好只有一个是 1（而不是两者都是 1）时将 1 赋给结果位。  `Not` 采用单个操作数并反转所有位（包括符号位），然后将该值赋予结果。  这意味着，对于有符号正数，`Not` 始终返回负值，而对于负数，`Not` 始终返回正值或零。  
  
 `AndAlso` 和 `OrElse` 运算符不支持按位运算。  
  
> [!NOTE]
>  只能对整型执行按位运算。  浮点值必须转换为整型后，才能执行按位运算。  
  
## 请参阅  
 [逻辑\/按位运算符](../../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [布尔表达式](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)   
 [算术运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [比较运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [串联运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)   
 [运算符的有效组合](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)