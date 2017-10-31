---
title: "如何：创建返回值的过程 (Visual Basic) | Microsoft Docs"
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
  - "过程, 定义"
  - "过程, 返回值"
  - "Visual Basic 代码, 过程"
ms.assetid: 8ee19f95-a9ef-4033-963b-d224dca207c4
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 如何：创建返回值的过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用 `Function` 过程将值返回给调用代码。  
  
### 创建返回值的过程  
  
1.  在任何其他过程之外，使用一条 `Function` 语句，后跟一条 `End Function` 语句。  
  
2.  在 `Function` 语句中，`Function` 关键字后跟过程名称，随后是放在括号中的参数列表。  
  
3.  在括号后跟 `As` 子句，以指定返回值的数据类型。  
  
4.  将过程的代码语句放在 `Function` 语句与 `End Function` 语句之间。  
  
5.  使用 `Return` 语句将值返回给调用代码。  
  
     下面的 `Function` 过程通过给定的直角三角形的两条直角边计算该三角形的最长边（即斜边）。  
  
     [!code-vb[VbVbcnProcedures#1](./codesnippet/VisualBasic/how-to-create-a-procedure-that-returns-a-value_1.vb)]  
  
     下面的示例演示对  `hypotenuse` 的典型调用。  
  
     [!code-vb[VbVbcnProcedures#6](./codesnippet/VisualBasic/how-to-create-a-procedure-that-returns-a-value_2.vb)]  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [如何：从过程返回值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-return-a-value-from-a-procedure.md)   
 [如何：调用返回值的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-returns-a-value.md)