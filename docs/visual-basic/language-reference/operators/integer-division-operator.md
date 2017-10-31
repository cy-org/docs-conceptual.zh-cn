---
title: "\ 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.\"
  - "\"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "\ 运算符 [Visual Basic]"
  - "算术运算符, 除法"
  - "反斜杠 (\) [Visual Basic]"
  - "除法运算符, integer"
  - "除法, 被零除"
  - "整除运算符"
  - "整数商"
  - "数学运算符"
  - "商, integer"
  - "截断, 整数除法"
  - "零, 被零除"
ms.assetid: 4b0ee347-950c-45c9-8e23-54bc85df208e
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# \ 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将两个数相除并返回以整数形式表示的结果。  
  
## 语法  
  
```  
  
expression1 \ expression2  
```  
  
## 部件  
 `expression1`  
 必选。  任何数值表达式。  
  
 `expression2`  
 必选。  任何数值表达式。  
  
## 支持的类型  
 所有数值类型，包括无符号和浮点类型以及 `Decimal`。  
  
## 结果  
 结果是 `expression1` 除以 `expression2` 的整数商，它丢弃了所有余数，只保留整数部分。  这称为“截断”。  
  
 结果数据类型是适用于 `expression1` 和 `expression2` 的数据类型的数值类型。  请参见 [运算符结果的数据类型](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md) 中的“整数算法”表。  
  
 [\/ 运算符](../../../visual-basic/language-reference/operators/floating-point-division-operator.md) 返回完整的商，将余数保留为小数形式。  
  
## 备注  
 在执行除法之前，Visual Basic 尝试将所有浮点数值表达式转换为 `Long`。  如果 `Option Strict` 为 `On`，将产生编译器错误。  如果 `Option Strict` 为 `Off`，若值超出 [Long 数据类型](../../../visual-basic/language-reference/data-types/long-data-type.md) 的范围，则可能会产生 <xref:System.OverflowException>。  转换为 `Long` 也服从“四舍六入五成双”。  有关更多信息，请参见 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md) 中的“小数部分”。  
  
 如果 `expression1` 或 `expression2` 计算结果等于 [Nothing](../../../visual-basic/language-reference/nothing.md)，则将其视为零。  
  
## 尝试用零作除数  
 如果 `expression2` 计算结果等于零，`\` 运算符将引发 <xref:System.DivideByZeroException> 异常。  对于所有数值数据类型的操作数也是如此。  
  
> [!NOTE]
>  `\` 运算符可以被“重载”，这意味着当操作数的类型为类或结构时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `\` 运算符执行整数除法。  结果是一个整数，表示两个操作数的整数商，余数被丢弃。  
  
 [!code-vb[VbVbalrOperators#18](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/integer-division-operator_1.vb)]  
  
 上例中的表达式分别返回值 2、3、33 和 \-22。  
  
## 请参阅  
 [\\\= 运算符](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)   
 [\/ 运算符](../../../visual-basic/language-reference/operators/floating-point-division-operator.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [算术运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)