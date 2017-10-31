---
title: "如何︰ 将过程传递给在 Visual Basic 中的另一个过程 |Microsoft 文档"
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
- AddressOf operator
- delegates [Visual Basic], passing procedures
ms.assetid: 5adbba15-5a1d-413f-ab3e-3ff6cc0a4669
caps.latest.revision: 9
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
ms.openlocfilehash: 9865e2d7d3786d289add3fa63b3db777317facdf
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-pass-procedures-to-another-procedure-in-visual-basic"></a>如何：在 Visual Basic 中将过程传递给另一过程
此示例演示如何使用委托来将过程传递给另一个过程。  
  
 委托是一种可以像任何其他类型中使用[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。 `AddressOf`运算符将返回一个委托对象时应用于过程的名称。  
  
 此示例中有一个具有委托参数可以采用另一个过程，使用获取的参考过程`AddressOf`运算符。  
  
### <a name="create-the-delegate-and-matching-procedures"></a>创建委托和匹配过程  
  
1.  创建名为委托`MathOperator`。  
  
     [!code-vb[VbVbalrDelegates #&1;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_1.vb)]  
  
2.  创建一个名为过程`AddNumbers`参数和返回值相匹配的`MathOperator`，以便签名匹配。  
  
     [!code-vb[VbVbalrDelegates #&2;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_2.vb)]  
  
3.  创建一个名为过程`SubtractNumbers`相匹配的签名与`MathOperator`。  
  
     [!code-vb[VbVbalrDelegates #&3;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_3.vb)]  
  
4.  创建一个名为过程`DelegateTest`采用委托作为参数。  
  
     此过程可以接受对引用`AddNumbers`或`SubtractNumbers`，因为它们的签名匹配`MathOperator`签名。  
  
     [!code-vb[VbVbalrDelegates #&4;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_4.vb)]  
  
5.  创建一个名为过程`Test`调用`DelegateTest`一次使用的委托`AddNumbers`作为参数，并再次使用的委托`SubtractNumbers`作为参数。  
  
     [!code-vb[VbVbalrDelegates #&5;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_5.vb)]  
  
     当`Test`是它调用，首先显示的结果`AddNumbers`活动上`5`和`3`，也就是 8。 然后的结果`SubtractNumbers`作用于`9`和`3`显示时，也就是 6。  
  
## <a name="see-also"></a>另请参阅  
 [委托](../../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [AddressOf 运算符](../../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Delegate 语句](../../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [如何：调用委托方法](../../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)
