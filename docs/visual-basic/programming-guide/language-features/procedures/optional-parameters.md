---
title: "可选参数 (Visual Basic) | Microsoft Docs"
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
  - "变量 [Visual Basic], 可选"
  - "命名的参数, 和可选参数"
  - "可选参数"
  - "可选参数, 和命名参数"
  - "Optional 关键字, 可选参数"
  - "可选参数"
  - "参数, 可选"
  - "过程, 可选参数"
  - "Visual Basic 代码, 过程"
ms.assetid: 398d2845-1069-4e94-b934-a73b545c8b87
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 可选参数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以指定过程参数是可选的，并且在调用过程时不必为其提供变量。  “可选参数”在过程定义中由关键字 `Optional` 指示。  适用以下规则：  
  
-   过程定义中的每个可选参数都必须指定默认值。  
  
-   可选参数的默认值必须是一个常数表达式。  
  
-   过程定义中跟在可选参数后的每个参数也都必须是可选的。  
  
 下面的语法显示带可选参数的过程声明：  
  
```  
Sub sub name(ByVal parameter1 As datatype1, Optional ByVal parameter2 As datatype2 = defaultvalue)  
```  
  
## 调用带可选参数的过程  
 调用带可选参数的过程时，可以选择是否提供该变量。  如果不提供，过程将使用为该参数声明的默认值。  
  
 当省略参数列表中的一个或多个可选参数时，使用连续的逗号来标记它们的位置。  下面的调用示例提供了第一个和第四个参数，省略了第二个和第三个：  
  
```  
  
sub name(argument 1, , , argument 4)  
```  
  
 下面的示例对 `MsgBox` 函数进行多次调用。  `MsgBox` 有一个必需参数和两个可选参数。  
  
 对 `MsgBox` 的第一个调用将按照 `MsgBox` 定义参数的顺序提供所有三个参数。  第二个调用仅提供必选参数。  第三个和第四个调用分别提供第一个和第三个参数。  第三个调用按位置提供参数，第四个调用按名称提供参数。  
  
 [!code-vb[VbVbcnProcedures#47](./codesnippet/VisualBasic/optional-parameters_1.vb)]  
  
## 确定可选参数是否存在  
 过程在运行时无法检测到给定的参数是否已被省略，或者调用代码是否已显式提供默认值。  如果需要弄清楚这一点，可以设置一个不可能的值作为默认值。  下面的过程定义了可选参数  `office`，并测试其默认值  `QJZ` 以查看它在调用中是否已被省略：  
  
 [!code-vb[VbVbcnProcedures#46](./codesnippet/VisualBasic/optional-parameters_2.vb)]  
  
 如果可选参数是像 `String` 这样的引用类型，只要它不是该变量所预期的值，就可以使用 `Nothing` 作为默认值。  
  
## 可选参数和重载  
 定义带可选参数的过程的另一种方法是使用重载。  如果有一个可选参数，可以定义过程的两个重载版本，一个接受此参数，另一个则不带参数。  此方法随可选参数数目的增加而变得更复杂。  然而，这样做的优点是可以完全确定调用程序是否提供了每个可选参数。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [通过值和通过引用传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [按位置和按名称传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [参数数组](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md)   
 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)