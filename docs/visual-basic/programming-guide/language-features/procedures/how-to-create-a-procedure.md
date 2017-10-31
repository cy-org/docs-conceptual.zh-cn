---
title: "如何：创建过程 (Visual Basic) | Microsoft Docs"
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
  - "过程声明"
  - "过程, 关于过程"
  - "过程, 定义"
  - "Visual Basic 代码, 过程"
  - "Visual Basic 代码, 重新使用"
ms.assetid: 4f779247-0b50-47e8-9e5c-ab5cf39ac0d2
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# 如何：创建过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

过程放在起始声明语句（`Sub` 或 `Function`）和结束声明语句（`End Sub` 或 `End Function`）之间。  过程的所有代码均位于这些语句之间。  
  
 一个过程中不能包含其他过程，因此其起始和结束语句必须位于其他任何过程之外。  
  
 如果您的代码需要在不同位置执行同样的任务，则可以将任务当作过程编写一次，然后就可以从代码的不同位置调用该任务。  
  
### 创建不返回值的过程  
  
1.  在其他任何过程之外，使用一条 `Sub` 语句，然后是一条 `End Sub` 语句。  
  
2.  在 `Sub` 语句中，`Sub` 关键字的后面为过程名，随后是位于括号中的参数列表。  
  
3.  过程的代码语句放在 `Sub` 语句与 `End Sub` 语句之间。  
  
### 创建返回值的过程  
  
1.  在任何其他过程之外，使用一条 `Function` 语句，后跟一条 `End Function` 语句。  
  
2.  在 `Function` 语句中，`Function` 关键字的后面为过程名，紧接着是位于括号中的参数列表，然后是指定返回值的数据类型的 `As` 子句。  
  
3.  将过程的代码语句放在 `Function` 语句与 `End Function` 语句之间。  
  
4.  使用 `Return` 语句将值返回给调用代码。  
  
### 将新过程与原来的重复性代码块连接起来  
  
1.  确保在原代码有权访问的地方定义新过程。  
  
2.  在原来的重复性代码块中，用一条调用 `Sub` 过程或 `Function` 过程的语句替换执行重复任务的语句。  
  
3.  如果过程是一个返回值的 `Function`，请确保调用语句使用返回值执行了某个操作（如将返回值存储在变量中），否则该值将丢失。  
  
## 示例  
 下面的 `Function` 过程通过给定的直角三角形的两条直角边计算该三角形的最长边（即斜边）。  
  
 [!code-vb[VbVbcnProcedures#1](./codesnippet/VisualBasic/how-to-create-a-procedure_1.vb)]  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [递归过程](../../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [面向对象的编程](../Topic/Object-Oriented%20Programming%20\(C%23%20and%20Visual%20Basic\).md)