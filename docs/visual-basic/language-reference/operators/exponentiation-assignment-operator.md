---
title: "^= 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.^="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "^= 运算符 [Visual Basic]"
  - "赋值语句, 复合"
  - "复合赋值语句"
  - "语句 [Visual Basic], 复合赋值"
ms.assetid: 397da132-2d96-4a85-a7bc-f7c730a608c9
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# ^= 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

进行以变量或属性的值为底、以表达式的值为幂的运算，并将结果赋回给该变量或属性。  
  
## 语法  
  
```  
  
variableorproperty ^= expression  
```  
  
## 部件  
 `variableorproperty`  
 必选。  任何数值变量或属性。  
  
 `expression`  
 必选。  任何数值表达式。  
  
## 备注  
 `^=` 运算符左边的元素可以是简单的标量变量，也可以是属性或数组元素。  变量或属性不能为 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。  
  
 `^=` 运算符首先引发该变量或属性的值 \(在运算符的左边\) 传递给表达式的值的幂 \(在运算符的右侧\)。  运算符然后将该操作的结果返回给变量或属性。  
  
 Visual Basic 总是以 [Double 数据类型](../../../visual-basic/language-reference/data-types/double-data-type.md) 形式执行求幂运算。  任何其他类型的操作数将转换为 `Double`，并且结果始终为 `Double`。  
  
 `expression` 的值可以是小数、负数，或负小数。  
  
## 重载  
 [^ 运算符](../../../visual-basic/language-reference/operators/exponentiation-operator.md) 可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  重载 `^` 运算符会影响 `^=` 运算符的行为。  如果代码在重载了 `^` 的类或结构上使用 `^=`，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `^=` 运算符进行以第一个 `Integer` 变量的值为底、以第二个变量的值为幂的运算，并将结果赋给第一个变量。  
  
 [!code-vb[VbVbalrOperators#21](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/exponentiation-assignment-operator_1.vb)]  
  
## 请参阅  
 [^ 运算符](../../../visual-basic/language-reference/operators/exponentiation-operator.md)   
 [赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)