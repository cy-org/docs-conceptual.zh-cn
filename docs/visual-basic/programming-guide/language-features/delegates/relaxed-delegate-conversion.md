---
title: "宽松委托转换 (Visual Basic 中) |Microsoft 文档"
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
- relaxed delegate conversion [Visual Basic]
- delegates [Visual Basic], relaxed conversion
- conversions, relaxed delegate
ms.assetid: 64f371d0-5416-4f65-b23b-adcbf556e81c
caps.latest.revision: 19
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
ms.openlocfilehash: c0160165d3df9755481b89570b4cd135b3a990a2
ms.lasthandoff: 03/13/2017

---
# <a name="relaxed-delegate-conversion-visual-basic"></a>宽松委托转换 (Visual Basic)
宽松的委托转换，您将子例程和函数分配给委托或处理程序，甚至当它们的签名不一致时。 因此，绑定到委托将与已允许的方法调用的绑定一致。  
  
## <a name="parameters-and-return-type"></a>参数和返回类型  
 替代签名完全匹配松散的转换需要满足以下条件时`Option Strict`设置为`On`:  
  
-   扩大转换为所分配函数的相应参数的数据类型必须存在从每个委托参数的数据类型或`Sub`。 在下面的示例中，该委托`Del1`具有一个参数、 `Integer`。 参数`m`在分配的 lambda 表达式必须具有从扩大转换的数据类型`Integer`，如`Long`或`Double`。  
  
     [!code-vb[VbVbalrRelaxedDelegates #&1;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_1.vb)]  
  
     [!code-vb[VbVbalrRelaxedDelegates #&2;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_2.vb)]  
  
     仅当允许收缩转换`Option Strict`设置为`Off`。  
  
     [!code-vb[VbVbalrRelaxedDelegates #&8;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_3.vb)]  
  
-   扩大转换中必须存在以相反方向从所分配函数的返回类型或`Sub`到委托的返回类型。 在下面的示例中，每个已分配的 lambda 表达式的主体必须计算结果为数据类型扩展到`Integer`因为的返回类型`del1`是`Integer`。  
  
     [!code-vb[VbVbalrRelaxedDelegates #&3;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_4.vb)]  
  
 如果`Option Strict`设置为`Off`、 扩大限制中两个方向将被删除。  
  
 [!code-vb[VbVbalrRelaxedDelegates #&4;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_5.vb)]  
  
## <a name="omitting-parameter-specifications"></a>忽略参数规范  
 宽松的委托还允许您将能够完全省略中分配的方法的参数规范︰  
  
 [!code-vb[VbVbalrRelaxedDelegates #&5;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_6.vb)]  
  
 [!code-vb[VbVbalrRelaxedDelegates #&6;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_7.vb)]  
  
 请注意，你不能指定某些参数，而忽略其他人。  
  
 [!code-vb[VbVbalrRelaxedDelegates #&15;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_8.vb)]  
  
 能够省略参数是在如定义一个事件处理程序，其中包含一些复杂参数的情况下很有帮助。 不使用某些事件处理程序的参数。 相反，该处理程序直接访问该事件在其注册，并忽略这些参数的控件的状态。 宽松的委托允许你忽略不产生多义性时此类声明中的参数。 在下面的示例中，完全指定的方法`OnClick`可以重写为`RelaxedOnClick`。  
  
```vb  
Sub OnClick(ByVal sender As Object, ByVal e As EventArgs) Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
  
Sub RelaxedOnClick() Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
```  
  
## <a name="addressof-examples"></a>AddressOf 示例  
 在前面的示例使用 lambda 表达式以便可以方便地查看类型关系。 但是，同一松弛法允许使用的委托分配`AddressOf`， `Handles`，或`AddHandler`。  
  
 在下面的示例中，函数`f1`， `f2`， `f3`，和`f4`都可以分配到`Del1`。  
  
 [!code-vb[VbVbalrRelaxedDelegates #&1;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_1.vb)]  
  
 [!code-vb[VbVbalrRelaxedDelegates #&7;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_9.vb)]  
  
 [!code-vb[VbVbalrRelaxedDelegates #&9;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_10.vb)]  
  
 下面的示例是仅当`Option Strict`设置为`Off`。  
  
 [!code-vb[VbVbalrRelaxedDelegates #&14;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_11.vb)]  
  
## <a name="dropping-function-returns"></a>删除函数返回值  
 宽松的委托转换使您能够分配到一个函数`Sub`委托时，有效地忽略该函数的返回值。 但是，不能分配`Sub`到一个函数委托。 在下面的示例中，函数的地址`doubler`分配给`Sub`委托`Del3`。  
  
 [!code-vb[VbVbalrRelaxedDelegates #&10;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_12.vb)]  
  
 [!code-vb[VbVbalrRelaxedDelegates #&11;](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/VisualBasic/relaxed-delegate-conversion_13.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [Lambda 表达式](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [委托](../../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [如何︰ 将过程传递给在 Visual Basic 中的另一个过程](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
