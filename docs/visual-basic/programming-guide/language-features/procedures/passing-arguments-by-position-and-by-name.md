---
title: "按位置和名称传递参数 (Visual Basic) | Microsoft Docs"
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
  - ":= 传递参数"
  - "参数传递"
  - "参数传递, 按位置"
  - "变量 [Visual Basic], 按名称列出"
  - "变量 [Visual Basic], 按名称传递"
  - "变量 [Visual Basic], 按位置传递"
  - "Function 过程, 传递参数"
  - "命名的参数"
  - "命名的参数, 传递参数"
  - "命名的参数"
  - "命名的参数, 传递参数"
  - "传递参数, 按名称"
  - "传递参数, 按位置"
  - "传递参数, 命名参数的参数"
  - "过程参数"
  - "过程, 参数"
  - "过程, 调用"
  - "Sub 过程, 传递参数"
  - "Visual Basic 代码, 过程"
ms.assetid: 1ad7358f-1da9-48da-a95b-f3c7ed41eff3
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 按位置和名称传递参数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

在调用 `Sub` 或 `Function` 过程时，可以“通过位置”传递参数（即按参数出现在过程定义中的顺序），或者“通过名称”传递参数而不考虑位置。  
  
 通过名称传递参数时，指定参数的声明名称，后接冒号和等号 \(`:=`\)，后面是参数值。  可以按照任意的顺序提供命名参数。  
  
 例如，下面的 `Sub` 过程带三个参数：  
  
 [!code-vb[VbVbcnProcedures#41](./codesnippet/VisualBasic/passing-arguments-by-position-and-by-name_1.vb)]  
  
 调用该过程时，可以通过位置、通过名称或者两者的混合来提供参数。  
  
## 通过位置传递参数  
 可以通过位置传递参数（以逗号分隔）来调用  `studentInfo`  过程，如下例所示：  
  
 [!code-vb[VbVbcnProcedures#42](./codesnippet/VisualBasic/passing-arguments-by-position-and-by-name_2.vb)]  
  
 如果在一个按位置排列的参数列表中省略可选参数，必须用逗号保留它的位置。  下面的示例调用没有  `age`  参数的  `studentInfo` ：  
  
 [!code-vb[VbVbcnProcedures#43](./codesnippet/VisualBasic/passing-arguments-by-position-and-by-name_3.vb)]  
  
## 通过名称传递参数  
 另一种方法是，可以通过名称传递参数（同样以逗号分隔）来调用  `studentInfo`  过程，如下例所示：  
  
 [!code-vb[VbVbcnProcedures#44](./codesnippet/VisualBasic/passing-arguments-by-position-and-by-name_4.vb)]  
  
## 通过位置和通过名称混合参数  
 在单个过程调用中，可以同时通过位置和通过名称提供参数，如下例所示：  
  
 [!code-vb[VbVbcnProcedures#45](./codesnippet/VisualBasic/passing-arguments-by-position-and-by-name_5.vb)]  
  
 在前面的示例中，由于  `birth`  是通过名称传递的，所以没有必要用额外的逗号来保留省略的  `age`  参数的位置。  
  
 如果同时通过位置和通过名称提供参数，定位参数都必须放在前面。  通过名称提供了一个参数后，其余的参数必须都通过名称提供。  
  
## 通过名称提供可选参数  
 当调用包含一个以上可选参数的过程时，通过名称传递参数尤其有用。  如果通过名称提供参数，则不必用连续的逗号表示缺少的定位参数。  通过名称传递参数也使跟踪正在传递和省略的参数变得更容易。  
  
## 通过名称提供参数方面的限制  
 通过名称传递参数不能避免输入必需的参数。  只能省略可选参数。  
  
 不能通过名称传递参数数组。  这是因为当调用过程时，为参数数组提供的参数数量不确定且以逗号分隔，而编译器无法将多个参数与单个名称关联。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [如何：将参数传递给过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [通过值和通过引用传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [可选参数](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [参数数组](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md)   
 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)