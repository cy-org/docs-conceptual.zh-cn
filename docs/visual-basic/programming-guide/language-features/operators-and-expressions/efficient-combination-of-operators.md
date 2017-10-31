---
title: "运算符的有效组合 (Visual Basic) | Microsoft Docs"
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
  - "表达式 [Visual Basic], 复杂"
  - "表达式 [Visual Basic], 运算符"
  - "表达式 [Visual Basic], 括号"
  - "数值表达式"
  - "运算符 [Visual Basic], 关联性"
  - "运算符 [Visual Basic], 复杂表达式"
  - "运算符 [Visual Basic], 优先级"
  - "括号, 复杂表达式"
  - "Visual Basic 代码, 表达式"
  - "Visual Basic 代码, 运算符"
ms.assetid: bd22340e-b5be-458b-8772-3916c02309a4
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 运算符的有效组合 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

复杂表达式可包含许多不同的运算符。  下面的示例阐释了这一点。  
  
 `x = (45 * (y + z)) ^ (2 / 85) * 5 + z`  
  
 创建前面示例中这样的复杂表达式要求彻底理解运算符优先级的规则。  有关更多信息，请参见 [Visual Basic 中的运算符优先级](../../../../visual-basic/language-reference/operators/operator-precedence.md)。  
  
## 加括号的表达式  
 经常需要以不同于运算符优先级所确定的顺序来执行运算。  请看下面的示例。  
  
 `x = z * y + 4`  
  
 前面的示例将 `z` 乘以 `y`，然后将结果与 `4` 相加。  但是，如果想要将 `y` 与 `4` 相加，然后再将结果与 `z` 相乘，您可以通过使用括号来重写常规运算符优先级。  通过将表达式放在括号中，将强制首先计算该表达式，而不管运算符优先级如何。  为了强制前面的示例先计算加法，您可以按以下示例中所示的方式重写该示例。  
  
 `x = z * (y + 4)`  
  
 前面的示例将 `y` 与 `4` 相加，然后再将和与 `z` 相乘。  
  
### 嵌套的带括号表达式  
 可以将表达式嵌套到多层括号中，以进一步重写优先级。  将首先计算嵌套在括号中最深层的表达式，然后计算下一个嵌套最深的表达式，依此类推计算到嵌套在最外层的表达式，最后计算括号外部的表达式。  下面的示例阐释了这一点。  
  
 `x = (z * 4) ^ (y * (z + 2))`  
  
 在前面的示例中，将首先计算 `z + 2` 的值，然后再计算其他带括号的表达式。  通常比加法或乘法具有更高优先级的求幂在此示例中最后计算，因为其他表达式都放在括号中。  
  
## 请参阅  
 [算术运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [比较运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Visual Basic 中的逻辑运算符和位运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)   
 [逻辑\/按位运算符](../../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [布尔表达式](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)   
 [值的比较](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [如何：计算数值](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-calculate-numeric-values.md)   
 [Visual Basic 中的运算符优先级](../../../../visual-basic/language-reference/operators/operator-precedence.md)