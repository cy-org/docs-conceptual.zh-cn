---
title: "如何：定义运算符 (Visual Basic) | Microsoft Docs"
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
  - "运算符过程, 关于运算符过程"
  - "运算符 [Visual Basic], 定义"
  - "运算符 [Visual Basic], 重载"
  - "过程, 定义"
  - "过程, 运算符"
  - "返回值, 运算符过程"
  - "语法, 运算符过程"
  - "Visual Basic 代码, 运算符"
  - "Visual Basic 代码, 过程"
ms.assetid: d4b0e253-092a-4e6e-9fe2-01f562140a29
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 如何：定义运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果您已经定义了一个类或结构，当两个操作数有一个或全部都属于该类或结构的类型时，可以定义某个标准运算符（如 `*`、`<>` 或 `And`）的行为。  
  
 将标准运算符定义为类或结构中的一个运算符过程。  所有运算符过程必须为 `Public` `Shared`。  
  
 在类或结构上定义一个运算符也称为重载运算符。  
  
## 示例  
 下面的示例为名为  `height` 的结构定义 `+` 运算符。  该结构的高度以英尺和英寸为单位。  1 英寸等于 2.54 厘米，1 英尺等于 12 英寸。  为了确保使用标准形式的值（英寸 \< 12.0），构造函数执行模为 12 的运算。  `+` 运算符使用此构造函数生成标准形式的值。  
  
 [!code-vb[VbVbcnProcedures#25](./codesnippet/VisualBasic/how-to-define-an-operator_1.vb)]  
  
 可以使用下面的代码测试结构  `height` 。  
  
 [!code-vb[VbVbcnProcedures#26](./codesnippet/VisualBasic/how-to-define-an-operator_2.vb)]  
  
 有关更多信息和示例，请参见 [Operator Overloading in Visual Basic 2005](http://go.microsoft.com/fwlink/?LinkId=101703)（Visual Basic 2005 中的运算符重载）。  
  
## 请参阅  
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [如何：定义转换运算符](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [如何：调用运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)   
 [如何：使用定义运算符的类](../../../../visual-basic/programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md)   
 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [如何：声明结构](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [Mod 运算符](../../../../visual-basic/language-reference/operators/mod-operator.md)