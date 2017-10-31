---
title: "如何：重载带有可选参数的过程 (Visual Basic) | Microsoft Docs"
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
  - "过程重载, 可选参数"
  - "过程参数"
  - "过程, 定义"
  - "过程, 多个版本"
  - "过程, 重载"
  - "过程, 参数"
  - "Visual Basic 代码, 过程"
ms.assetid: 825f9d56-4cde-43fd-993a-b9171717e2eb
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 如何：重载带有可选参数的过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果过程具有一个或多个 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md) 参数，就无法定义与它的任何隐式重载匹配的重载版本。  有关更多信息，请参见 [重载过程注意事项](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md) 中的“可选参数的隐式重载”。  
  
## 一个可选参数  
  
#### 重载带有一个可选参数的过程  
  
1.  编写参数列表中包含可选参数的 `Sub` 或 `Function` 声明语句。  不要在此重载版本中使用 `Optional` 关键字。  
  
2.  在 `Sub` 或 `Function` 关键字的前面使用 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md) 关键字。  
  
3.  编写在调用代码提供可选参数时应执行的过程代码。  
  
4.  根据需要，用 `End Sub` 或 `End Function` 语句终止过程。  
  
5.  写入第二个声明语句，除了参数列表中不包含可选参数以外，它与第一个声明完全相同。  
  
6.  编写在调用代码不提供可选参数时应执行的过程代码。  根据需要，用 `End Sub` 或 `End Function` 语句终止过程。  
  
     下面的示例演示定义了可选参数的过程、与此等效的两个重载过程，以及无效和有效重载版本的最终示例。  
  
     [!code-vb[VbVbcnProcedures#59](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-optional-parameters_1.vb)]  
  
     [!code-vb[VbVbcnProcedures#60](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-optional-parameters_2.vb)]  
  
     [!code-vb[VbVbcnProcedures#61](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-optional-parameters_3.vb)]  
  
## 多个可选参数  
 带有多个可选参数的过程通常需要两个以上的重载版本。  例如，如果有两个可选参数，而且调用代码可以独立提供或省略每一个参数，那么需要有四个重载版本，所提供参数的每个可能的组合都需要使用一个版本。  
  
 随着可选参数数量的增加，重载的复杂性随之增加。  除非所提供参数的一些组合不可接受，否则 N 个可选参数需要 2 ^ N 个重载版本。  根据过程的特性，您会发现定义所有重载版本的额外努力是十分值得的。  
  
#### 重载带有多个可选参数的过程  
  
1.  确定所提供可选参数的哪些组合对于过程逻辑来说是可以接受的。  如果一个可选参数依赖于另一个可选参数，便可能出现不可接受的组合。  例如，如果一个参数接受了一个配偶的姓名，另一个参数接受了配偶的年龄，那么提供年龄但省略姓名的参数组合就不可接受。  
  
2.  对于所提供可选参数的每个可接受组合，应编写 `Sub` 或 `Function` 声明语句，定义对应的参数列表。  不要使用 `Optional` 关键字。  
  
3.  在每个声明中，将 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md) 关键字放在 `Sub` 或 `Function` 关键字的前面。  
  
4.  在每个声明的后面，编写在调用代码提供与该声明的参数列表对应的变量列表时应当执行的过程代码。  
  
5.  根据需要，用 `End Sub` 或 `End Function` 语句终止每个过程。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [可选参数](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [参数数组](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [过程疑难解答](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [如何：定义一个过程的多个版本](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [如何：调用重载过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-overloaded-procedure.md)   
 [如何：重载参数数量不确定的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [重载决策](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)