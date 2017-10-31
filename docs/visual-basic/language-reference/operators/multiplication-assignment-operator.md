---
title: "*= 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.*="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "*= 运算符 [Visual Basic]"
  - "赋值语句, 复合"
  - "复合赋值语句"
  - "运算符 *="
  - "语句 [Visual Basic], 复合赋值"
ms.assetid: 96c86509-6eb8-4682-8226-3852e049376f
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# *= 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

变量或属性值乘以表达式值，并将结果赋给该变量或属性。  
  
## 语法  
  
```  
  
variableorproperty *= expression  
```  
  
## 部件  
 `variableorproperty`  
 必选。  任何数值变量或属性。  
  
 `expression`  
 必选。  任何数值表达式。  
  
## 备注  
 `*=` 运算符左边的元素可以是简单的标量变量，也可以是属性或数组元素。  变量或属性不能为 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。  
  
 `*=` 运算符首先使用该表达式的值 \(在运算符的右侧\) 和变量或属性的值 \(在运算符的左边\)。  运算符然后将该操作的结果赋给变量或属性。  
  
## 重载  
 [\* 运算符](../../../visual-basic/language-reference/operators/multiplication-operator.md) 可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  重载 `*` 运算符会影响 `*=` 运算符的行为。  如果代码在重载了 `*` 的类或结构上使用 `*=`，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `*=` 运算符，将一个 `Integer` 变量与第二个该变量相乘，并将结果赋给第一个变量。  
  
 [!code-vb[VbVbalrOperators#5](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/multiplication-assignment-operator_1.vb)]  
  
## 请参阅  
 [\* 运算符](../../../visual-basic/language-reference/operators/multiplication-operator.md)   
 [赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)