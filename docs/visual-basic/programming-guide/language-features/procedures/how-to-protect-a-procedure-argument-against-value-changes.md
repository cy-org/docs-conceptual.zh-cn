---
title: "如何︰ 防止过程参数的值被更改 (Visual Basic 中) |Microsoft 文档"
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
- procedures, arguments
- procedures, parameters
- procedure arguments
- arguments [Visual Basic], passing by reference
- Visual Basic code, procedures
- arguments [Visual Basic], ByVal
- arguments [Visual Basic], passing by value
- procedure parameters
- procedures, calling
- arguments [Visual Basic], ByRef
- arguments [Visual Basic], changing value
ms.assetid: d2b7c766-ce16-4d2c-8d79-3fc0e7ba2227
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
ms.openlocfilehash: 6e18f7ceefeec9c1f422d0eae4e727700ebd8b6e
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-protect-a-procedure-argument-against-value-changes-visual-basic"></a>如何：防止过程自变量的值被更改 (Visual Basic)
如果过程声明将参数作为[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]使过程代码中调用代码参数的基础的编程元素直接引用。 这将允许更改基础调用代码中的参数的值的过程。 在某些情况下调用的代码可能想要防止出现这种更改。  
  
 您可以始终防止参数更改通过声明的相应参数[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)过程中。 如果您想要将无法更改在某些情况下，而不是其他中给定的参数，可以将它声明`ByRef`，并让调用代码确定每个调用中的传递机制。 做到这一点通过将相应实参括在圆括号中以将其传递的值，或不将其括在圆括号中以通过引用传递。 有关详细信息，请参阅[如何︰ 强制通过值传递到参数](./how-to-force-an-argument-to-be-passed-by-value.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示两个过程可采用一个数组变量并运行它的元素。 `increase`过程只需添加一个对每个元素。 `replace`过程将一个新数组分配给该参数`a()`，然后添加一个对每个元素。 但是，重新分配不影响调用代码中的基础数组变量。  
  
 [!code-vb[VbVbcnProcedures #&35;](./codesnippet/VisualBasic/how-to-protect-a-procedure-argument-against-value-changes_1.vb)]  
  
 [!code-vb[VbVbcnProcedures #&38;](./codesnippet/VisualBasic/how-to-protect-a-procedure-argument-against-value-changes_2.vb)]  
  
 [!code-vb[VbVbcnProcedures #&37;](./codesnippet/VisualBasic/how-to-protect-a-procedure-argument-against-value-changes_3.vb)]  
  
 第一个`MsgBox`调用显示"之后 increase(n): 11、 21、 31、 41"。 因为数组`n`是引用类型，`replace`可以更改其中一个成员，即使传递机制是`ByVal`。  
  
 第二个`MsgBox`调用显示"之后 replace(n): 11、 21、 31、 41"。 因为`n`传递`ByVal`，`replace`不能修改该变量`n`通过向它分配一个新数组，调用代码中。 当`replace`创建新的数组实例`k`并将其分配给本地变量`a`，它将失去对引用`n`由调用代码传入的。 当其更改的成员`a`，只有本地数组`k`受到影响。 因此，`replace`不会增加数组的值`n`调用代码中。  
  
## <a name="compiling-the-code"></a>编译代码  
 中的默认设置[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]是按值传递参数。 但是，很好的编程做法包括[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)或[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)关键字用于声明的每个参数。 这使您的代码易于阅读。  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [如何︰ 将参数传递给过程](./how-to-pass-arguments-to-a-procedure.md)   
 [通过值和通过引用传递参数](./passing-arguments-by-value-and-by-reference.md)   
 [可修改和不可修改参数之间的差异](./differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [通过值和通过引用传递参数之间的差异](./differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [如何︰ 更改过程参数的值](./how-to-change-the-value-of-a-procedure-argument.md)   
 [如何︰ 强制通过值传递参数](./how-to-force-an-argument-to-be-passed-by-value.md)   
 [按位置和按名称传递参数](./passing-arguments-by-position-and-by-name.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
