---
title: "如何︰ 将参数传递给过程 (Visual Basic 中) |Microsoft 文档"
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
- arguments [Visual Basic], passing to procedures
- procedures, arguments
- procedures, parameters
- procedure arguments
- Visual Basic code, procedures
- procedure parameters
- procedures, calling
- argument passing, procedures
ms.assetid: 08723588-3890-4ddc-8249-79e049e0f241
caps.latest.revision: 14
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
ms.openlocfilehash: ddccd476b2347368d0435f637edf3882db306f45
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-pass-arguments-to-a-procedure-visual-basic"></a>如何：将自变量传递给过程 (Visual Basic)
当调用过程时，过程名后面加上括号中的参数列表。 不提供参数对应于每个所需的参数定义了该过程，并可以选择提供参数`Optional`参数。 如果不提供`Optional`中调用的参数，必须包括逗号来标记其位置在参数列表中的，如果要提供任何后续的参数。  
  
 如果您想要的参数传递的数据类型不同于其对应的参数，如`Byte`到`String`，可设置类型检查开关 ([Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) 到`Off`。 如果`Option Strict`是`On`，则必须使用扩大转换或显式转换的关键字。 有关详细信息，请参阅[扩大和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)和[类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)。  
  
 有关详细信息，请参阅[过程参数和变量](./procedure-parameters-and-arguments.md)。  
  
### <a name="to-pass-one-or-more-arguments-to-a-procedure"></a>若要将一个或多个参数传递给过程  
  
1.  在调用的语句中，请按照带括号的过程名称。  
  
2.  在括号内，将参数列表。 包括每个所需的参数的参数定义了该过程，并且用逗号分隔参数。  
  
3.  请确保每个参数是一个有效表达式，计算结果为数据类型转换为该过程的类型定义的相应参数。  
  
4.  如果参数定义为[可选](../../../../visual-basic/language-reference/modifiers/optional.md)，您可以将其包括在参数列表或省略此参数。 如果省略此参数，该过程将使用定义为该参数的默认值。  
  
5.  如果省略一个参数`Optional`参数并且没有另一个参数在它后面的参数列表中，您可以将省略参数的位置标记的参数列表中一个多余的逗号。  
  
     下面的示例调用[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]<xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>函数。</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>  
  
     [!code-vb[VbVbcnProcedures #&34;](./codesnippet/VisualBasic/how-to-pass-arguments-to-a-procedure_1.vb)]  
  
     前面的示例中提供所需的第一个参数，这是要显示的消息字符串。 它会省略了可选的第二个参数，它指定要在消息框上显示的按钮的参数。 调用不会提供一个值，因为`MsgBox`使用默认值， `MsgBoxStyle.OKOnly`，后者将只显示**确定**按钮。  
  
     在参数列表中的第二个逗号标记省略的第二个参数的位置和最后一个的字符串传递给第三个可选参数`MsgBox`，即在标题栏中显示的文本。  
  
## <a name="see-also"></a>另请参阅  
 [Sub 过程](./sub-procedures.md)   
 [Function 过程](./function-procedures.md)   
 [属性过程](./property-procedures.md)   
 [运算符过程](./operator-procedures.md)   
 [如何︰ 为过程定义参数](./how-to-define-a-parameter-for-a-procedure.md)   
 [通过值和通过引用传递参数](./passing-arguments-by-value-and-by-reference.md)   
 [递归过程](./recursive-procedures.md)   
 [过程重载](./procedure-overloading.md)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [面向对象的编程](http://msdn.microsoft.com/library/1cf6e655-3f30-45f1-9a5d-4a88ca24a1c2)
