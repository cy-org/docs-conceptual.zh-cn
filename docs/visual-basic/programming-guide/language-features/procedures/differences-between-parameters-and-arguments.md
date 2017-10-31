---
title: "参数和变量之间的差异 (Visual Basic) | Microsoft Docs"
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
  - "变量 [Visual Basic], 和参数"
  - "参数, 和变量"
  - "参数, 定义"
  - "过程参数"
  - "过程参数"
  - "过程, 参数"
  - "过程, 参数"
  - "Visual Basic 代码, 过程"
ms.assetid: c237c056-74f4-4749-9f2c-15864f139a31
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 参数和变量之间的差异 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

多数情况下，过程必须包含有关调用环境的一些信息。  执行重复或共享任务的过程对每次调用使用不同的信息。  此信息包含每次调用过程时传递给它的变量、常量和表达式。  
  
 若要将此信息传递给过程，过程先要定义一个形参，然后调用代码将一个实参传递给所定义的形参。  您可以将形参当作一个停车位，而将实参当作一辆汽车。  就像一个停车位可以在不同时间停放不同的汽车一样，调用代码在每次调用过程时可以将不同的实参传递给同一个形参。  
  
## 参数  
 形参表示一个值，过程希望您在调用它时传递该值。  过程的声明定义过程的参数。  
  
 当您定义 `Function` 或 `Sub` 过程时，需要在紧跟过程名称的括号内指定形参列表。  对于每个形参，您可以指定名称、数据类型和传入机制（[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 或 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)）。  您还可以指示某个形参是可选的。  这意味着调用代码不必传递它的值。  
  
 每个形参的名称均可作为过程内的局部变量。  形参名称的使用方法与其他任何变量的使用方法相同。  
  
## 参数  
 实参表示在您调用过程时传递给过程形参的值。  调用代码在调用过程时提供参数。  
  
 调用 `Function` 或 `Sub` 过程时，需要在紧跟过程名称的括号内包括实参列表。  每个实参均与此列表中位于相同位置的那个形参相对应。  
  
 与形参定义不同，实参没有名称。  每个实参就是一个表达式，它包含零或多个变量、常数和文本。  求值的表达式的数据类型通常应与为相应形参定义的数据类型相匹配，并且在任何情况下，该表达式值都必须可转换为此形参类型。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [如何：为过程定义参数](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-parameter-for-a-procedure.md)   
 [如何：将参数传递给过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [通过值和通过引用传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [递归过程](../../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)