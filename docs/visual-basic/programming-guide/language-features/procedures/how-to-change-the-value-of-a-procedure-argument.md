---
title: "如何︰ 更改过程参数 (Visual Basic 中) 的值 |Microsoft 文档"
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
- arguments [Visual Basic], ByRef
- arguments [Visual Basic], changing value
ms.assetid: 6fad2368-5da7-4c07-8bf8-0f4e65a1be67
caps.latest.revision: 16
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
ms.openlocfilehash: 6c42a50b75bcc70ae0a3f70771b9e1f85626004b
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-change-the-value-of-a-procedure-argument-visual-basic"></a>如何：更改过程自变量的值 (Visual Basic)
当调用过程时，您提供每个参数对应一个过程中定义的参数。 在某些情况下，过程代码可以更改基础调用代码中的参数的值。 在其他情况下，该过程可以更改只有一个参数的本地副本。  
  
 当您调用过程中，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]使传递的每个参数的本地副本[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)。 对于每个参数传递[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]使过程代码中调用代码参数的基础的编程元素直接引用。  
  
 如果调用代码中的基础元素是一个可修改的元素，则参数进行传递`ByRef`，过程代码可用于直接引用更改调用代码中的元素的值。  
  
## <a name="changing-the-underlying-value"></a>更改基础值  
  
#### <a name="to-change-the-underlying-value-of-a-procedure-argument-in-the-calling-code"></a>若要更改过程参数的调用代码中的基础值  
  
1.  在过程声明中，指定[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)对应于参数的参数。  
  
2.  在调用代码中，将作为参数传递的可修改的编程元素。  
  
3.  在调用代码中，不要将括在圆括号中的参数列表中的参数。  
  
4.  在过程代码中，使用参数名称将值分配给调用代码中的基础元素。  
  
 请参阅示例进一步向下的演示。  
  
## <a name="changing-local-copies"></a>不断变化的本地副本  
 如果调用代码中的基础元素是不可更改的元素，或者如果传递参数`ByVal`，过程将无法更改它调用的代码中的值。 但是，该过程可以更改此类实际参数的本地副本。  
  
#### <a name="to-change-the-copy-of-a-procedure-argument-in-the-procedure-code"></a>若要更改过程参数在过程代码中的副本  
  
1.  在过程声明中，指定[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)对应于参数的参数。  
  
     - 或 -  
  
     在调用代码中，将括在圆括号中的参数列表中的参数。 这样做可以强制[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]来按值传递参数，即使相应的参数指定`ByRef`。  
  
2.  在过程代码中，使用参数名称将值分配给该参数的本地副本。 不更改基础值调用的代码中。  
  
## <a name="example"></a>示例  
 下面的示例演示两个过程可采用一个数组变量并运行它的元素。 `increase`过程只需添加一个对每个元素。 `replace`过程将一个新数组分配给该参数`a()`，然后添加一个对每个元素。  
  
 [!code-vb[VbVbcnProcedures #&35;](./codesnippet/VisualBasic/how-to-change-the-value-of-a-procedure-argument_1.vb)]  
  
 [!code-vb[VbVbcnProcedures #&36;](./codesnippet/VisualBasic/how-to-change-the-value-of-a-procedure-argument_2.vb)]  
  
 [!code-vb[VbVbcnProcedures #&37;](./codesnippet/VisualBasic/how-to-change-the-value-of-a-procedure-argument_3.vb)]  
  
 第一个`MsgBox`调用显示"后 increase(n): 11、 21、 31、 41"。 因为数组`n`是引用类型，`replace`可以更改其中一个成员，即使传递机制是`ByVal`。  
  
 第二个`MsgBox`调用显示"之后 replace(n): 101、 201、 301"。 因为`n`传递`ByRef`，`replace`可以修改变量`n`中调用代码并将赋给它一个新数组。 因为`n`是引用类型，`replace`还可以更改它的成员。  
  
 您可以防止该过程修改调用代码中的变量本身。 请参阅[如何︰ 防止过程参数的值被更改](./how-to-protect-a-procedure-argument-against-value-changes.md)。  
  
## <a name="compiling-the-code"></a>编译代码  
 当通过引用传递变量时，则必须使用`ByRef`关键字来指定此机制。  
  
 中的默认设置[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]是按值传递参数。 但是，很好的编程做法包括[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)或[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)关键字用于声明的每个参数。 这使您的代码易于阅读。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 在允许一个过程来更改基础调用代码中的参数的值都具有潜在的风险。 请确保您希望此值可更改，并做好准备，然后再使用它的有效性检查它。  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [如何︰ 将参数传递给过程](./how-to-pass-arguments-to-a-procedure.md)   
 [通过值和通过引用传递参数](./passing-arguments-by-value-and-by-reference.md)   
 [可修改和不可修改参数之间的差异](./differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [通过值和通过引用传递参数之间的差异](./differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [如何︰ 防止过程参数的值更改](./how-to-protect-a-procedure-argument-against-value-changes.md)   
 [如何︰ 强制通过值传递参数](./how-to-force-an-argument-to-be-passed-by-value.md)   
 [按位置和按名称传递参数](./passing-arguments-by-position-and-by-name.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
