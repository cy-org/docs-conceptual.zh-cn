---
title: "&amp;= 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.&="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "&= 运算符 [Visual Basic]"
  - "赋值语句, 复合"
  - "复合赋值语句"
  - "运算符 &="
  - "语句 [Visual Basic], 复合赋值"
ms.assetid: 0cf262fc-1a05-419a-a503-60013f111c8a
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# &amp;= 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

连接 `String` 表达式与 `String` 变量或属性，并将结果赋给该变量或属性。  
  
## 语法  
  
```  
  
variableorproperty &= expression  
```  
  
## 部件  
 `variableorproperty`  
 必选。  任何 `String` 变量或属性。  
  
 `expression`  
 必选。  任何 `String` 表达式。  
  
## 备注  
 `&=` 运算符左边的元素可以是简单的标量变量，也可以是属性或数组元素。  变量或属性不能为 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。  `&=` 运算符连接在其右侧的 `String` 在其左侧的表达式。 `String` 变量或属性，然后将在其左侧的结果赋给变量或属性。  
  
## 重载  
 [& 运算符](../../../visual-basic/language-reference/operators/concatenation-operator.md) 可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  重载 `&` 运算符会影响 `&=` 运算符的行为。  如果代码在重载了 `&` 的类或结构上使用 `&=`，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `&=` 运算符将两个 `String` 变量连接，并将结果赋给第一个变量。  
  
 [!code-vb[VbVbalrOperators#3](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/and-assignment-operator_1.vb)]  
  
## 请参阅  
 [& 运算符](../../../visual-basic/language-reference/operators/concatenation-operator.md)   
 [\+\= 运算符](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)   
 [赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [串联运算符](../../../visual-basic/language-reference/operators/concatenation-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)