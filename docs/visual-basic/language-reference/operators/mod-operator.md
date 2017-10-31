---
title: "Mod 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Mod"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "余数（Mod 运算符）"
  - "除法运算符，Mod 运算符"
  - "取模运算符，Visual Basic"
  - "Mod 运算符 [Visual Basic]"
  - "运算符 [Visual Basic]，除号"
  - "算术运算符，Mod"
  - "数学运算符"
ms.assetid: 6ff7e40e-cec8-4c77-bff6-8ddd2791c25b
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Mod 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将两个数字相除并且仅返回余数。  
  
## 语法  
  
```  
  
number1 Mod number2  
```  
  
## 部件  
 `number1`  
 必需。  任何数值表达式。  
  
 `number2`  
 必需。  任何数值表达式。  
  
## 支持的类型  
 所有数值类型。  这包括无符号类型和浮点类型以及 `Decimal`。  
  
## 结果  
 结果为 `number1` 除以 `number2` 后的余数。  例如，表达式 `14 Mod 4` 的结果为 2。  
  
## 备注  
 如果 `number1` 或 `number2` 是浮点值，则将返回除法运算的浮点余数。  结果的数据类型是最小的数据类型，该类型可以容纳由 `number1` 和 `number2` 的数据类型相除得到的所有可能值。  
  
 如果 `number1` 或 `number2` 计算结果等于 [Nothing](../../../visual-basic/language-reference/nothing.md)，则将其视为零。  
  
 相关的运算符包括：  
  
-   [\\ 运算符](../../../visual-basic/language-reference/operators/integer-division-operator.md) 返回除法运算的整数商。  例如，表达式 `14 \ 4` 的结果为 3。  
  
-   [\/ 运算符](../../../visual-basic/language-reference/operators/floating-point-division-operator.md) 返回包括余数在内的完整商，为浮点数。  例如，表达式 `14 / 4` 的结果为 3.5。  
  
## 尝试用零作除数  
 如果 `number2` 等于零，则 `Mod` 运算符的行为取决于操作数的数据类型。  整数除法引发 <xref:System.DivideByZeroException> 异常。  浮点数除法返回 <xref:System.Double.NaN>。  
  
## 等效公式  
 表达式 `a Mod b` 与下面的公式是等价的：  
  
 `a - (b * (a \ b))`  
  
 `a - (b * Fix(a / b))`  
  
## 浮点数偏差  
 在处理浮点数字时，请记住浮点数在内存中并不总是有精确的表示形式。  对于某些操作（例如值比较和 `Mod` 运算符），这可能导致意外的结果。  有关更多信息，请参见[数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)。  
  
## 重载  
 `Mod` 运算符可进行重载，这意味着类或结构可以重定义其行为。  如果您在代码中将 `Mod` 应用到包含此类重载的类或结构的实例中，请确保您了解其重定义的行为。  有关更多信息，请参见[运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `Mod` 运算符将两个数相除，并只返回余数。  如果有一个数是浮点数，则结果是表示余数的浮点数。  
  
 [!code-vb[VbVbalrOperators#31](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/mod-operator_1.vb)]  
  
## 示例  
 下面的示例演示了浮点操作数潜在的不精确性。  在第一个语句中，操作数的类型为 `Double`，0.2 是一个存储的值为 0.20000000000000001 的无限重复的二进制小数。  在第二个语句中，文本类型字符 `D` 将两个操作数强制为 `Decimal` 类型，0.2 具有精确的表示形式。  
  
 [!code-vb[VbVbalrOperators#32](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/mod-operator_2.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Conversion.Int%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Fix%2A>   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [算术运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [\\ 运算符](../../../visual-basic/language-reference/operators/integer-division-operator.md)