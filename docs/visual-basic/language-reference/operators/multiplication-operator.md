---
title: "* 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.*"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "* 运算符 [Visual Basic]"
  - "算术运算符, 乘法"
  - "数学运算符"
  - "乘法运算符, 语法"
  - "运算符 [Visual Basic], 乘法"
ms.assetid: 2b210382-99da-4195-89ba-b1d06f5e89ad
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# * 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将两个数相乘。  
  
## 语法  
  
```  
  
number1 * number2  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`number1`|必选。  任何数值表达式。|  
|`number2`|必选。  任何数值表达式。|  
  
## 结果  
 结果是 `number1` 和 `number2` 的乘积。  
  
## 支持的类型  
 所有数值类型，包括无符号和浮点类型以及 `Decimal`。  
  
## 备注  
 所得结果的数据类型取决于操作数的类型。  下表显示如何确定结果的数据类型。  
  
|||  
|-|-|  
|操作数数据类型|结果数据类型|  
|两个表达式都是整数数据类型（[SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)、[Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md)、[Short](../../../visual-basic/language-reference/data-types/short-data-type.md)、[UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md)、[Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md)、[UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)、[Long](../../../visual-basic/language-reference/data-types/long-data-type.md)、[ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)）|适合 `number1` 和 `number2` 数据类型的 Numeric 数据类型。  请参见 [运算符结果的数据类型](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md) 中的“整数算法”表。|  
|两个表达式都是 [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md)|`Decimal`|  
|两个表达式都是 [Single](../../../visual-basic/language-reference/data-types/single-data-type.md)|`Single`|  
|每个表达式都为浮点数据类型（`Single` 或 [Double](../../../visual-basic/language-reference/data-types/double-data-type.md)）但不能都是 `Single`（注意，`Decimal` 不是浮点数据类型）|`Double`|  
  
 如果表达式的计算结果为 [Nothing](../../../visual-basic/language-reference/nothing.md)，则将其视为零。  
  
## 重载  
 `*` 运算符可以被重载，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 本示例使用 `*` 运算符将两个数相乘。  结果是两个操作数的乘积。  
  
 [!code-vb[VbVbalrOperators#4](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/multiplication-operator_1.vb)]  
  
## 请参阅  
 [\*\= 运算符](../../../visual-basic/language-reference/operators/multiplication-assignment-operator.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [算术运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)