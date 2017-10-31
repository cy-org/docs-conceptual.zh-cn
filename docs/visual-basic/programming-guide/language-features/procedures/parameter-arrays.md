---
title: "参数数组 (Visual Basic) | Microsoft Docs"
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
  - "变量 [Visual Basic], 参数数组"
  - "数组 [Visual Basic], 参数数组"
  - "ParamArray 关键字, 参数数组"
  - "参数数组, 关于参数数组"
  - "参数, 参数数组"
  - "过程, 不确定数量的参数值"
  - "Visual Basic 代码, 过程"
ms.assetid: c43edfae-9114-4096-9ebc-8c5c957a1067
caps.latest.revision: 26
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 26
---
# 参数数组 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通常，不能超出过程声明指定调用带有多个参数的过程。  如果需要参数时的不确定数字，可以声明 *参数*数组，它允许过程接受参数的值。  ，在定义过程时，不必知道参数数组中的元素数。  每个单独确定数组的大小调用该过程。  
  
## 声明 ParamArray  
 使用 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) 关键字表示中的参数数组。  适用以下规则:  
  
-   程序只能定义一个参数数组，因此，它必须是过程定义中的最后一个参数。  
  
-   参数数组必须通过值传递。  好的编程做法是显式使用关键字 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 在过程定义。  
  
-   参数数组是自动可选的。  其默认值为参数数组元素类型的空一维数组。  
  
-   必需的参数数组前面的所有参数。  参数数组必须是唯一的可选参数。  
  
## 调用 ParamArray  
 当您调用定义参数数组的过程时，可以在任何一种方式提供参数以下方式所示:  
  
-   不提供任何参数，即可以省略 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) 参数。  在这种情况下，一个空数组传递给过程。  您还可以传递 [Nothing](../../../../visual-basic/language-reference/nothing.md) 关键字，具有相同的效果。  
  
-   任意数量的参数列表，以逗号分隔。  每个参数的数据类型必须可以隐式转换为 `ParamArray` 元素类型。  
  
-   与元素类型的数组与参数数组的元素类型相同。  
  
 在任何情况下，过程中的代码将参数数组，一维数组与数据类型的元素和 `ParamArray` 数据类型相同。  
  
> [!IMPORTANT]
>  每当处理可能变得无限大的数组，有耗尽应用程序的某些内部容量的风险。  如果接受一个参数数组，则应该测试调用代码传递给它的数组的大小。  ，如果它对于应用程序来说太大，请执行适当的操作。  有关更多信息，请参见 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)。  
  
## 示例  
 下面的示例定义并调用函数 `calcSum`。  参数的 `args``ParamArray` 修饰符使该函数接受参数数目可变。  
  
 [!code-vb[VbVbalrStatements#26](../../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/parameter-arrays_1.vb)]  
  
 下面的示例定义带有参数数组的一个过程所有数组元素的值传递给参数数组。  
  
 [!code-vb[VbVbcnProcedures#48](./codesnippet/VisualBasic/parameter-arrays_2.vb)]  
  
 [!code-vb[VbVbcnProcedures#49](./codesnippet/VisualBasic/parameter-arrays_3.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Information.UBound%2A>   
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [通过值和通过引用传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [按位置和按名称传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [可选参数](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md)