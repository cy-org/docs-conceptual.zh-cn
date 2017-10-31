---
title: "异或运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Xor"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "按位比较"
  - "按位运算符, XOR 运算符"
  - "“异”运算符"
  - "异或运算符"
  - "逻辑异"
  - "运算符 [Visual Basic], 按位"
  - "运算符 [Visual Basic], 异或"
  - "Xor 关键字"
  - "异或运算符 [Visual Basic]"
ms.assetid: 036000a9-3934-4e7f-a9d0-a816de3d84a6
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 异或运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对两个 `Boolean` 表达式执行逻辑异或运算，或对两个数值表达式执行按位异或运算。  
  
## 语法  
  
```  
  
result = expression1 Xor expression2  
```  
  
## 部件  
 `result`  
 必选。  任何 `Boolean` 或数值变量。  对于 Boolean 比较，`result` 是两个 `Boolean` 值的逻辑异或运算（互斥逻辑析取）。  对于按位运算，`result` 是代表两个数值位组合模式的按位异或运算（互斥按位析取）的数值。  
  
 `expression1`  
 必选。  任何 `Boolean` 或数值表达式。  
  
 `expression2`  
 必选。  任何 `Boolean` 或数值表达式。  
  
## 备注  
 对于 Boolean 比较，当且仅当 `expression1` 和 `expression2` 的计算结果之一正好为 `True` 时，`result` 为 `True`。  即，当且仅当 `expression1` 和 `expression2` 计算结果为相反的 `Boolean` 值时。  下表演示如何确定 `result`。  
  
|如果 `expression1` 为|并且 `expression2` 为|`result` 的值为|  
|------------------------|------------------------|------------------|  
|`True`|`True`|`False`|  
|`True`|`False`|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
> [!NOTE]
>  在 Boolean 比较中，`Xor` 运算符总是计算两个表达式，其中可能包括调用过程。  `Xor` 没有相应的短路式运算符，因为结果总是取决于两个操作数。  有关“短路式”逻辑运算符，请参见 [AndAlso 运算符](../../../visual-basic/language-reference/operators/andalso-operator.md) 和 [OrElse 运算符](../../../visual-basic/language-reference/operators/orelse-operator.md)。  
  
 对于按位运算，`Xor` 运算符对两个数值表达式中的位置相同的位执行按位比较，并且按下表设置 `result` 中的相应位。  
  
|如果 `expression1` 中的位为|并且 `expression2` 中的位为|`result` 中的位为|  
|---------------------------|---------------------------|-------------------|  
|1|1|0|  
|1|0|1|  
|0|1|1|  
|0|0|0|  
  
> [!NOTE]
>  因为逻辑和按位运算符的优先级低于其他算术和关系运算符，所以应将任何按位运算括在括号中以确保准确执行。  
  
 例如，5 `Xor` 3 等于 6。  如果要知道其中的来龙去脉，可将 5 和 3 转化为其二进制表示形式 101 和 011，  然后利用前面表格中的规则，可确定 101 Xor 011 等于 110，此结果是十进制数 6 的二进制表示形式。  
  
## 数据类型  
 如果操作数由一个 `Boolean` 表达式和一个数值表达式组成，则 Visual Basic 将 `Boolean` 表达式转换为数值（–1 表示 `True`，0 表示 `False`），然后执行按位运算。  
  
 对于 `Boolean` 比较，结果的数据类型为 `Boolean`。  对于按位比较，结果数据类型是适用于 `expression1` 和 `expression2` 的数据类型的 numeric 类型。  请参见 [运算符结果的数据类型](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md) 中的表“关系与按位比较”。  
  
## 重载  
 `Xor` 运算符可以被重载，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `Xor` 运算符对两个表达式执行逻辑异或运算（互斥逻辑析取）。  结果是一个 `Boolean` 值，它表示两个表达式中是否只有一个的结果为 `True`。  
  
 [!code-vb[VbVbalrOperators#40](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xor-operator_1.vb)]  
  
 上面的示例分别产生结果 `False`、`True` 和 `False`。  
  
## 示例  
 下面的示例使用 `Xor` 运算符对两个数值表达式的各个位执行逻辑异或运算（互斥逻辑析取）。  如果操作数中的相应位仅有一个被设置为 1，则结果模式中的位被设置。  
  
 [!code-vb[VbVbalrOperators#41](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xor-operator_2.vb)]  
  
 上面的示例分别产生结果 2、12 和 14。  
  
## 请参阅  
 [逻辑\/按位运算符](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Visual Basic 中的逻辑运算符和位运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)