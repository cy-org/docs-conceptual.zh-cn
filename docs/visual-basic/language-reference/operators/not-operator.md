---
title: "Not 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Not"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "按位比较"
  - "按位运算符, NOT 运算符"
  - "Boolean 表达式, 非"
  - "变量中的反位值"
  - "逻辑非"
  - "非运算符"
  - "Not 运算符 [Visual Basic]"
  - "运算符 [Visual Basic], 按位"
  - "运算符 [Visual Basic], 非"
ms.assetid: 8f2ea83c-d2ed-480a-a474-3042a1cad9b5
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# Not 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对 `Boolean` 表达式执行逻辑求反，或对数值表达式执行按位求反。  
  
## 语法  
  
```  
  
result = Not expression  
```  
  
## 部件  
 `result`  
 必选。  任何 `Boolean` 或数值表达式。  
  
 `expression`  
 必选。  任何 `Boolean` 或数值表达式。  
  
## 备注  
 对于 `Boolean` 表达式，下表说明如何确定 `result`。  
  
|如果 `expression` 为|`result` 的值为|  
|-----------------------|------------------|  
|`True`|`False`|  
|`False`|`True`|  
  
 对于数值表达式，`Not` 运算符将任何数值表达式的位值反转，并且根据下表设置 `result` 中的相应位。  
  
|如果 `expression` 中的位为|`result` 中的位为|  
|--------------------------|-------------------|  
|1|0|  
|0|1|  
  
> [!NOTE]
>  因为逻辑和按位运算符的优先级低于其他算术和关系运算符，所以应将任何按位运算括在括号中以确保准确执行。  
  
## 数据类型  
 对于布尔值求反运算，结果的数据类型为 `Boolean`。  对于按位求反运算，结果的数据类型与 `expression` 的数据类型一样。  然而，如果表达式是 `Decimal` 类型，则结果为 `Long` 类型。  
  
## 重载  
 `Not` 运算符可以被重载，这意味着当该运算符的操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `Not` 运算符对 `Boolean` 表达式执行逻辑求反。  结果是表示与表达式的值相反的 `Boolean` 值。  
  
 [!code-vb[VbVbalrOperators#33](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/not-operator_1.vb)]  
  
 上面的示例分别产生结果 `False` 和 `True`。  
  
## 示例  
 下面的示例使用 `Not` 运算符对数值表达式的各个位执行逻辑求反。  结果模式中的位被设置为操作数模式中的相应位的相反值，包括符号位。  
  
 [!code-vb[VbVbalrOperators#34](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/not-operator_2.vb)]  
  
 上面的示例分别产生结果 \-11、\-9 和 \-7。  
  
## 请参阅  
 [逻辑\/按位运算符](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Visual Basic 中的逻辑运算符和位运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)