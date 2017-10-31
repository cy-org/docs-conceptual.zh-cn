---
title: "And 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.And"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "And 运算符 [Visual Basic]"
  - "按位 AND 运算符 [Visual Basic]"
  - "按位比较"
  - "按位运算符, AND 运算符"
  - "连接运算符"
  - "逻辑与"
  - "运算符 [Visual Basic], 按位"
  - "运算符 [Visual Basic], 连接"
ms.assetid: 2ea711f3-439a-4c7c-9e3a-1ffe3b0d6046
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# And 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对两个 `Boolean` 表达式执行逻辑合取，或对两个数值表达式执行按位合取。  
  
## 语法  
  
```  
  
result = expression1 And expression2  
```  
  
## 部件  
 `result`  
 必选。  任何 `Boolean` 或数值表达式。  对于 Boolean 比较，`result` 是对两个 `Boolean` 值的逻辑合取。  对于按位运算，`result` 是一个表示两个数位组合模式的按位合取的数值。  
  
 `expression1`  
 必选。  任何 `Boolean` 或数值表达式。  
  
 `expression2`  
 必选。  任何 `Boolean` 或数值表达式。  
  
## 备注  
 对于 Boolean 比较，当且仅当 `expression1` 和 `expression2` 的计算结果都为 `True` 时，`result` 为 `True`。  下表演示如何确定 `result`。  
  
|如果 `expression1` 为|并且 `expression2` 为|`result` 的值为|  
|------------------------|------------------------|------------------|  
|`True`|`True`|`True`|  
|`True`|`False`|`False`|  
|`False`|`True`|`False`|  
|`False`|`False`|`False`|  
  
> [!NOTE]
>  在 Boolean 比较中，`And` 运算符始终计算两个表达式，表达式可以包括过程调用。  [AndAlso 运算符](../../../visual-basic/language-reference/operators/andalso-operator.md) 执行“短路”，这意味着如果 `expression1` 为 `False`，则不计算 `expression2`。  
  
 当应用于数值时，`And` 运算符对两个数值表达式中位置相同的位执行按位比较，并且按下表设置 `result` 中的对应位：  
  
|如果 `expression1` 中的位为|并且 `expression2` 中的位为|`result` 中的位为|  
|---------------------------|---------------------------|-------------------|  
|1|1|1|  
|1|0|0|  
|0|1|0|  
|0|0|0|  
  
> [!NOTE]
>  因为逻辑和按位运算符的优先级低于其他算术和关系运算符，所以应将所有按位运算括在括号中以确保准确的计算结果。  
  
## 数据类型  
 如果操作数由一个 `Boolean` 表达式和一个数值表达式组成，则 Visual Basic 将 `Boolean` 表达式转换为数值（–1 表示 `True`，0 表示 `False`），然后执行按位运算。  
  
 对于 Boolean 比较，结果的数据类型为 `Boolean`。  对于按位比较，结果数据类型是适用于 `expression1` 和 `expression2` 的数据类型的 numeric 类型。  请参见 [运算符结果的数据类型](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md) 中的表“关系与按位比较”。  
  
> [!NOTE]
>  `And` 运算符可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `And` 运算符对两个表达式执行逻辑合取。  结果是一个 `Boolean` 值，它表示两个表达式是否都为 `True`。  
  
 [!code-vb[VbVbalrOperators#22](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/and-operator_1.vb)]  
  
 上面的示例分别产生结果 `True` 和 `False`。  
  
## 示例  
 下面的示例使用 `And` 运算符对两个数值表达式的各位执行逻辑合取。  如果两个操作数中的对应位都被设置为 1，则结果模式中的位也被置位。  
  
 [!code-vb[VbVbalrOperators#23](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/and-operator_2.vb)]  
  
 上面的示例分别产生结果 8、2 和 0。  
  
## 请参阅  
 [逻辑\/按位运算符](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [AndAlso 运算符](../../../visual-basic/language-reference/operators/andalso-operator.md)   
 [Visual Basic 中的逻辑运算符和位运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)