---
title: "如何︰ 强制通过值 (Visual Basic 中) 传递参数 |Microsoft 文档"
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
- Visual Basic code, procedures
- arguments [Visual Basic], ByVal
- arguments [Visual Basic], passing by value
- procedure parameters
- procedures, calling
- arguments [Visual Basic], in parentheses
- procedure arguments, in parentheses
- arguments [Visual Basic], changing value
ms.assetid: 77b4f2d2-1055-4c2f-a521-874d1db86946
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
ms.openlocfilehash: eea3466534f1797170ae4bc72afbcba899929911
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-force-an-argument-to-be-passed-by-value-visual-basic"></a>如何：强制通过值传递自变量 (Visual Basic)
过程声明确定传递机制。 如果在声明参数[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]期望通过引用传递相应的参数。 这允许更改调用代码中的实参的编程元素的值的过程。 如果你想要防止此类更改基础元素，则可以重写`ByRef`传递机制在过程中的调用的参数名称括在括号内。 这些括号是除了括号之外的参数列表的调用中。  
  
 调用代码不能重写[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)机制。  
  
### <a name="to-force-an-argument-to-be-passed-by-value"></a>若要强制通过值传递参数  
  
-   如果对应的形参声明为`ByVal`在过程中，不需要采取任何额外的步骤。 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]已经期望通过值传递参数。  
  
-   如果对应的形参声明为`ByRef`在过程中，将括在圆括号中的过程调用参数。  
  
## <a name="example"></a>示例  
 下面的示例重写`ByRef`参数声明。 在强制调用`ByVal`，请注意括号的两个级别。  
  
 [!code-vb[VbVbcnProcedures #&39;](./codesnippet/VisualBasic/how-to-force-an-argument-to-be-passed-by-value_1.vb)]  
  
 [!code-vb[VbVbcnProcedures #&40;](./codesnippet/VisualBasic/how-to-force-an-argument-to-be-passed-by-value_2.vb)]  
  
 当`str`括在参数列表中的额外括号中`setNewString`过程不能更改在调用代码中，其值和`MsgBox`显示"无法替换如果传递 ByVal"。 当`str`不括在额外的圆括号，过程可以更改它，和`MsgBox`显示"这是 inString 参数的一个新值"。  
  
## <a name="compiling-the-code"></a>编译代码  
 当通过引用传递变量时，则必须使用`ByRef`关键字来指定此机制。  
  
 中的默认设置[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]是按值传递参数。 但是，很好的编程做法包括[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)或[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)关键字用于声明的每个参数。 这使您的代码易于阅读。  
  
## <a name="robust-programming"></a>可靠编程  
 如果过程声明参数[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)，正确的执行代码的可能依赖于能够更改调用代码中的基础元素。 如果调用代码重写此调用的机制，通过将实参括在括号内，或者如果它通过一个不可修改参数，该过程不能更改基础元素。 这可能会产生意外的结果调用的代码中。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 在允许一个过程来更改基础调用代码中的参数的值都具有潜在的风险。 请确保您希望此值可更改，并做好准备，然后再使用它的有效性检查它。  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [如何︰ 将参数传递给过程](./how-to-pass-arguments-to-a-procedure.md)   
 [通过值和通过引用传递参数](./passing-arguments-by-value-and-by-reference.md)   
 [可修改和不可修改参数之间的差异](./differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [通过值和通过引用传递参数之间的差异](./differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [如何︰ 更改过程参数的值](./how-to-change-the-value-of-a-procedure-argument.md)   
 [如何︰ 防止过程参数的值更改](./how-to-protect-a-procedure-argument-against-value-changes.md)   
 [按位置和按名称传递参数](./passing-arguments-by-position-and-by-name.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
