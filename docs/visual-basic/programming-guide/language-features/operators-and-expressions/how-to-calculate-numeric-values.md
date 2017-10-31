---
title: "如何︰ 计算数值 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- operator precedence
- operators [Visual Basic]
- expressions [Visual Basic], numeric
- calculations, numeric expressions
- precedence, of operators
- Visual Basic code, operators
- Visual Basic code, expressions
- numeric expressions
ms.assetid: ba6bf43d-bd96-49b8-b1de-4a7797551372
caps.latest.revision: 13
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d844e2af3892d897125e21d3fd7047a8b295d10a
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-calculate-numeric-values-visual-basic"></a>如何：计算数值 (Visual Basic)
您可以计算通过使用数值表达式的数值。 一个*数值表达式*一个表达式，包含文本、 常量和变量表示数值，以及处理这些值的运算符。  
  
## <a name="calculating-numeric-values"></a>计算数值  
  
#### <a name="to-calculate-a-numeric-value"></a>若要计算的数字值  
  
-   将一个或多个数字文本、 常量和变量组合到一个数值表达式。 下面的示例显示了一些有效的数值表达式。  
  
     `93.217`  
  
     `System.Math.PI`  
  
     `counter`  
  
     `4 * (67 + i)`  
  
     前三行显示文本、 常量和变量。 每个构成有效的数值表达式本身。 最后一行演示具有两个字符串的变量的组合。  
  
     请注意，并未数值表达式组成的完整[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]本身的语句。 作为一个完整的语句的一部分，必须使用表达式。  
  
#### <a name="to-store-a-numeric-value"></a>若要存储的数字值  
  
-   赋值语句可用于将分配给一个变量，数值表达式所表示的值，如下面的示例所示。  
  
     [!code-vb[VbVbalrOperators #&82;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-calculate-numeric-values_1.vb)]  
  
     在前面的示例中，相等运算符右侧的表达式的值 (`=`) 赋给变量`j`运算符，左侧以便`j`的计算结果为 276。  
  
     有关详细信息，请参阅[语句](../../../../visual-basic/language-reference/statements/index.md)。  
  
## <a name="multiple-operators"></a>多个运算符  
 如果数值表达式包含多个运算符，它们的计算顺序由运算符优先级的规则确定。 若要覆盖的运算符优先顺序规则，则将表达式括在括号内，如上面的示例;首先计算括起来的表达式。  
  
#### <a name="to-override-normal-operator-precedence"></a>若要重写常规运算符优先级  
  
-   使用括号括住您想要首先执行的操作。 下面的示例演示具有相同的操作数和运算符的两个不同的结果。  
  
     [!code-vb[VbVbalrOperators #&83;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-calculate-numeric-values_2.vb)]  
  
     在前面的示例中，用于计算`j`执行加法运算符 (`+`) 第一个因为两边的括号`(67 + i)`正常的优先级和赋予的值重写`j`为 276 (4 次 69)。 用于计算`k`按常规优先级执行运算符 (`*`之前`+`)，和赋予的值`k`为 270 （268 加 2）。  
  
     有关详细信息，请参阅[Visual Basic 中的运算符优先级](../../../../visual-basic/language-reference/operators/operator-precedence.md)。  
  
## <a name="see-also"></a>请参见  
 [运算符和表达式](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [值的比较](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [语句](../../../../visual-basic/language-reference/statements/index.md)   
 [在 Visual Basic 中的运算符优先级](../../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [算术运算符](../../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [运算符的有效组合](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)
