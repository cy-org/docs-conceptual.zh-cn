---
title: "OrElse 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "OrElse"
  - "vb.OrElse"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "运算符 [Visual Basic], 析取"
  - "运算符 [Visual Basic], 短路处理"
  - "OrElse 运算符 [Visual Basic]"
  - "短路计算"
  - "短路处理"
ms.assetid: 253803d8-05b0-47d7-b213-abd222847779
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# OrElse 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对两个表达式执行短路包含逻辑析取。  
  
## 语法  
  
```  
  
result = expression1 OrElse expression2  
```  
  
## 部件  
 `result`  
 必选。  任何 `Boolean` 表达式。  
  
 `expression1`  
 必选。  任何 `Boolean` 表达式。  
  
 `expression2`  
 必选。  任何 `Boolean` 表达式。  
  
## 备注  
 如果编译的代码可以根据一个表达式的计算结果跳过对另一表达式的计算，则将该逻辑运算称为“短路”。  如果第一个表达式的计算结果可以决定运算的最终结果，则不需要计算另一个表达式，因为它不会更改最终结果。  如果跳过的表达式很复杂或涉及过程调用，则短路可以提高性能。  
  
 如果其中一个表达式或两个表达式的计算结果为 `True`，则 `result` 为 `True`。  下表演示如何确定 `result`。  
  
|如果 `expression1` 为|并且 `expression2` 为|`result` 的值为|  
|------------------------|------------------------|------------------|  
|`True`|（不计算）|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
## 数据类型  
 仅为 [Boolean 数据类型](../../../visual-basic/language-reference/data-types/boolean-data-type.md) 定义 `OrElse` 运算符。  Visual Basic 根据需要将每个操作数转换为 `Boolean` 并完全按 `Boolean` 类型执行运算。  如果将计算结果分配给数值类型，Visual Basic 会将结果从 `Boolean` 类型转换为数值类型，  这样可能会产生意想不到的行为。  例如，将 `5 OrElse 12` 转换为 `Integer` 时，将产生 `–1`。  
  
## 重载  
 可以“重载”[Or 运算符](../../../visual-basic/language-reference/operators/or-operator.md) 和 [IsTrue 运算符](../../../visual-basic/language-reference/operators/istrue-operator.md)，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  重载 `Or` 和 `IsTrue` 运算符会影响 `OrElse` 运算符的行为。  如果代码在重载了 `Or` 和 `IsTrue` 的类或结构上使用 `OrElse`，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `OrElse` 运算符对两个表达式执行逻辑析取。  结果是一个 `Boolean` 值，它表示两个表达式中是否有一个为真。  如果第一个表达式为 `True`，则不计算第二个表达式。  
  
 [!code-vb[VbVbalrOperators#37](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/orelse-operator_1.vb)]  
  
 上面的示例分别产生结果 `True`、`True` 和 `False`。  在计算 `firstCheck` 的过程中，因为第一个表达式已经为 `True`，所以不计算第二个表达式。  但是，在计算 `secondCheck` 时将计算第二个表达式。  
  
## 示例  
 下面的示例演示一个包含两个过程调用的 `If`...`Then` 语句。  如果第一个调用返回 `True`，则不调用第二个过程。  如果第二个过程执行运行此节代码时应始终执行的重要任务，这将产生意外结果。  
  
 [!code-vb[VbVbalrOperators#38](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/orelse-operator_2.vb)]  
  
## 请参阅  
 [逻辑\/按位运算符](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Or 运算符](../../../visual-basic/language-reference/operators/or-operator.md)   
 [IsTrue 运算符](../../../visual-basic/language-reference/operators/istrue-operator.md)   
 [Visual Basic 中的逻辑运算符和位运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)