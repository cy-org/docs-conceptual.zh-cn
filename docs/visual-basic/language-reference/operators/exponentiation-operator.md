---
title: "^ 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.^"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "^ 运算符 [Visual Basic]"
  - "^ 运算符 [Visual Basic], 幂"
  - "算术运算符, 幂"
  - "指数"
  - "exponentiation 运算符 [Visual Basic]"
  - "数字, 放样"
  - "幂"
  - "将数字提升到幂"
  - "平方运算符"
ms.assetid: d89a1ca8-83da-4784-a87b-a9d7dceb3f62
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# ^ 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

求以某个数为底、以另一个数为指数的幂。  
  
## 语法  
  
```  
  
number ^ exponent  
```  
  
## 部件  
 `number`  
 必选。  任何数值表达式。  
  
 `exponent`  
 必选。  任何数值表达式。  
  
## 结果  
 结果总是 `Double` 类型的以 `number` 为底、以 `exponent` 为指数的幂运算值。  
  
## 支持的类型  
 `Double`.  任何其他类型的操作数将转换为 `Double`。  
  
## 备注  
 Visual Basic 总是以 [Double 数据类型](../../../visual-basic/language-reference/data-types/double-data-type.md) 形式执行求幂运算。  
  
 `exponent` 的值可以是分数、负数或负分数。  
  
 如果在单个表达式中执行多个求幂运算，则按 `^` 运算符从左到右出现的顺序进行计算。  
  
> [!NOTE]
>  `^` 运算符可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `^` 运算符对一个数和一个指数进行求幂运算。  结果是以第一个操作数为底、以第二个操作数为指数的求幂运算的值。  
  
 [!code-vb[VbVbalrOperators#20](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/exponentiation-operator_1.vb)]  
  
 上面的示例产生下列结果：  
  
 `exp1` 的结果为 4（2 的平方）。  
  
 `exp2` 的结果为 19683（先求 3 的立方，再对得到的值求立方）。  
  
 `exp3` 的结果为 \-125（\-5 的立方）。  
  
 `exp4` 的结果为 625（\-5 的四次方）。  
  
 `exp5` 的结果为 2（8 的立方根）。  
  
 `exp6` 的结果为 0.5（1.0 除以 8 的立方根）。  
  
 请注意在上面示例的表达式中括号的重要性。  按照运算符优先级，Visual Basic 通常先执行 `^` 运算符，然后执行任何其他运算符，一元 `–` 运算符也不例外。  如果 `exp4` 和 `exp6` 计算时不带括号，将会产生下面的结果：  
  
 `exp4 = -5 ^ 4` 将计算 \(5 到第四个电源\)，导致 \-625。  
  
 `exp6 = 8 ^ -1.0 / 3.0` 将按“（8 的 –1 次幂，即 0.125）除以 3.0”进行计算，得到的结果为 0.041666666666666666666666666666667。  
  
## 请参阅  
 [^\= 运算符](../../../visual-basic/language-reference/operators/exponentiation-assignment-operator.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [算术运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)