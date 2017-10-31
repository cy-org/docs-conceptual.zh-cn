---
title: "&lt;&lt;= 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.<<="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "<<= 运算符 [Visual Basic]"
  - "赋值语句, 复合"
  - "复合赋值语句"
  - "运算符 <<="
  - "运算符 <<="
  - "语句 [Visual Basic], 复合赋值"
ms.assetid: 8ad26613-faff-4e2f-89ee-63feee33bfda
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# &lt;&lt;= 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对变量或属性值执行数学左移位，并将结果赋回给该变量或属性。  
  
## 语法  
  
```  
  
variableorproperty <<= amount  
```  
  
## 部件  
 `variableorproperty`  
 必选。  整型 \(`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long` 或 `ULong`\) 的变量或属性。  
  
 `amount`  
 必选。  数据类型扩展到 `Integer` 的数字表达式。  
  
## 备注  
 `<<=` 运算符左边的元素可以是简单的标量变量，也可以是属性或数组元素。  变量或属性不能为 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。  
  
 `<<=` 运算符首先对变量或属性的值进行数学左移。  运算符然后将该操作的结果返回到该变量或属性。  
  
 数学移位不是循环的，即不会将在结果的一端移出的数位从另一端重新移入。  在数学左移位运算中，丢弃移出结果数据类型范围的数位，而将右端空出的数位位置设置为零。  
  
## 重载  
 [\<\< 运算符](../../../visual-basic/language-reference/operators/left-shift-operator.md) 可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  重载 `<<` 运算符会影响 `<<=` 运算符的行为。  如果代码在重载了 `<<` 的类或结构上使用 `<<=`，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `<<=` 运算符将 `Integer` 变量的位模式向左移动指定的位数，并将结果赋给该变量。  
  
 [!code-vb[VbVbalrOperators#13](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/left-shift-assignment-operator_1.vb)]  
  
## 请参阅  
 [\<\< 运算符](../../../visual-basic/language-reference/operators/left-shift-operator.md)   
 [赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [移位运算符](../../../visual-basic/language-reference/operators/bit-shift-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)