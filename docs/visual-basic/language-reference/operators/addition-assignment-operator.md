---
title: "+= 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.+="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "+= 运算符 [Visual Basic]"
  - "+= 运算符 [Visual Basic], 追加字符串"
  - "赋值语句, 复合"
  - "复合赋值语句"
  - "语句 [Visual Basic], 复合赋值"
ms.assetid: d3e959f4-85d4-4e47-87c4-77b62335a5b3
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# += 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将一个数值表达式的值与一个数值变量或属性的值相加，并将结果赋给该变量或属性。  还可以用于将一个 `String` 表达式与一个 `String` 变量或属性连接在一起，并将此结果赋给该变量或属性。  
  
## 语法  
  
```  
  
variableorproperty += expression  
```  
  
## 部件  
 `variableorproperty`  
 必选。  任何数值或 `String` 变量或属性。  
  
 `expression`  
 必选。  任何数值或 `String` 表达式。  
  
## 备注  
 `+=` 运算符左边的元素可以是简单的标量变量，也可以是属性或数组元素。  变量或属性不能为 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。  
  
 `+=` 运算符将其右侧的在其左侧的值赋给变量或属性，然后将在其左侧的结果赋给变量或属性。  `+=` 运算符还可以使用联接在其右侧的 `String` 在其左侧的表达式。 `String` 变量或属性，然后将在其左侧的结果赋给变量或属性。  
  
> [!NOTE]
>  使用 `+=` 运算符时，可能无法确定应该执行加法运算还是执行字符串连接运算。  所以应使用 `&=` 运算符执行连接操作，以消除多义性并提供自我说明代码。  
  
 如果编译环境强制使用严格的语义，则此赋值运算符将隐式地执行扩大转换而不是收缩转换。  有关这些转换的更多信息，请参见 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  有关严格语义和宽松语义的更多信息，请参见 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)。  
  
 如果允许宽松语义，则 `+=` 运算符将隐式执行各种字符串和数值转换，与 `+` 运算符执行的转换相同。  有关这些转换的详细信息，请参见 [\+ 运算符](../../../visual-basic/language-reference/operators/addition-operator.md)。  
  
## 重载  
 `+` 运算符可以被“重载”，这意味着当操作数的类型为类或结构时，该类或结构可以重新定义其行为。  重载 `+` 运算符会影响 `+=` 运算符的行为。  如果代码在重载了 `+` 的类或结构上使用 `+=`，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `+=` 运算符将一个变量的值与另一个变量的值合并。  第一部分使用带有数值变量的 `+=`，将一个值与另一个值相加。  第二部分使用带有 `String` 变量的 `+=`，将一个值与另一个值连接在一起。  两个示例中的结果都赋给了第一个变量。  
  
 [!code-vb[VbVbalrOperators#7](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-assignment-operator_1.vb)]  
  
 [!code-vb[VbVbalrOperators#8](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-assignment-operator_2.vb)]  
  
 现在 `num1` 的值为 13，而 `str1` 的值为“103”。  
  
## 请参阅  
 [\+ 运算符](../../../visual-basic/language-reference/operators/addition-operator.md)   
 [赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [串联运算符](../../../visual-basic/language-reference/operators/concatenation-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)