---
title: "如何：定义转换运算符 (Visual Basic) | Microsoft Docs"
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
  - "运算符重载"
  - "运算符 [Visual Basic], 定义"
  - "运算符 [Visual Basic], 重载"
  - "过程, 定义"
  - "过程, 运算符"
  - "返回值, 运算符过程"
ms.assetid: 54203dfa-c24b-463f-9942-d5153e89e762
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 如何：定义转换运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果已定义了类或结构，则可以定义类或结构的类型与其他数据类型（如 `Integer`、`Double` 或 `String`）之间的类型转换运算符。  
  
 将类型转换定义为类型或结构中的 [CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md) 过程。  所有转换过程必须为 `Public Shared`，并且每个转换过程必须指定 [Widening](../../../../visual-basic/language-reference/modifiers/widening.md) 或 [Narrowing](../../../../visual-basic/language-reference/modifiers/narrowing.md)。  
  
 在类或结构上定义一个运算符也称为重载运算符。  
  
## 示例  
 下面的示例定义名称为  `digit`  的结构与 `Byte` 之间的转换运算符。  
  
 [!code-vb[VbVbcnProcedures#27](./codesnippet/VisualBasic/how-to-define-a-conversion-operator_1.vb)]  
  
 可以使用下面的代码测试结构 `digit`。  
  
 [!code-vb[VbVbcnProcedures#28](./codesnippet/VisualBasic/how-to-define-a-conversion-operator_2.vb)]  
  
## 请参阅  
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [如何：定义运算符](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [如何：调用运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)   
 [如何：使用定义运算符的类](../../../../visual-basic/programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md)   
 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [如何：声明结构](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [隐式转换和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)