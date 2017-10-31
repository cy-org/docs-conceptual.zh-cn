---
title: "AndAlso 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AndAlso"
  - "AndAlso"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "AndAlso 运算符"
  - "运算符 [Visual Basic], 连接"
  - "运算符 [Visual Basic], 短路处理"
  - "短路计算"
  - "短路处理"
ms.assetid: bbc15191-b374-495b-9b8f-7b8c2f4388eb
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# AndAlso 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对两个表达式执行简化逻辑合取。  
  
## 语法  
  
```  
  
result = expression1 AndAlso expression2  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`result`|必选。  任何 `Boolean` 表达式。  结果是比较两个表达式的 `Boolean` 结果。|  
|`expression1`|必选。  任何 `Boolean` 表达式。|  
|`expression2`|必选。  任何 `Boolean` 表达式。|  
  
## 备注  
 如果编译的代码可以根据一个表达式的计算结果跳过对另一表达式的计算，则将该逻辑运算称为“短路”。  如果第一个表达式的计算结果可以决定运算的最终结果，则不需要计算另一个表达式，因为它不会更改最终结果。  如果跳过的表达式很复杂或涉及过程调用，则短路可以提高性能。  
  
 如果两个表达式的计算结果均为 `True`，则 `result` 为 `True`。  下表演示如何确定 `result`。  
  
||||  
|-|-|-|  
|如果 `expression1` 为|并且 `expression2` 为|`result` 的值为|  
|`True`|`True`|`True`|  
|`True`|`False`|`False`|  
|`False`|（不计算）|`False`|  
  
## 数据类型  
 只为 [Boolean 数据类型](../../../visual-basic/language-reference/data-types/boolean-data-type.md) 定义 `AndAlso` 运算符。  Visual Basic 根据需要将每个操作数转换为 `Boolean` 并完全按 `Boolean` 类型执行运算。  如果将计算结果分配给数值类型，Visual Basic 会将结果从 `Boolean` 类型转换为数值类型，  这样可能会产生意想不到的行为。  例如，当 `5 AndAlso 12` 转换为 `Integer` 时，会得到 `–1`。  
  
## 重载  
 [And 运算符](../../../visual-basic/language-reference/operators/and-operator.md) 和 [IsFalse 运算符](../../../visual-basic/language-reference/operators/isfalse-operator.md) 运算符可以被重载，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  重载 `And` 和 `IsFalse` 运算符将影响 `AndAlso` 运算符的行为。  如果代码在重载了 `And` 和 `IsFalse` 的类或结构上使用 `AndAlso`，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `AndAlso` 运算符对两个表达式执行逻辑合取。  结果是一个 `Boolean` 值，它表示整个联合表达式是否为真。  如果第一个表达式为 `False`，则不计算第二个表达式。  
  
 [!code-vb[VbVbalrOperators#24](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/andalso-operator_1.vb)]  
  
 上述示例分别产生结果 `True`、`False` 和 `False`。  在 `secondCheck` 计算中，不计算第二个表达式，因为第一个表达式已经为 `False`。  但是，在 `thirdCheck` 计算中，要计算第二个表达式。  
  
## 示例  
 下面的示例演示一个 `Function` 过程，该过程在数组元素中搜索指定值。  如果此数组为空，或者搜索数目超出了数组长度，则 `While` 语句不会根据搜索值测试数组元素。  
  
 [!code-vb[VbVbalrOperators#25](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/andalso-operator_2.vb)]  
  
## 请参阅  
 [逻辑\/按位运算符](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [And 运算符](../../../visual-basic/language-reference/operators/and-operator.md)   
 [IsFalse 运算符](../../../visual-basic/language-reference/operators/isfalse-operator.md)   
 [Visual Basic 中的逻辑运算符和位运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)