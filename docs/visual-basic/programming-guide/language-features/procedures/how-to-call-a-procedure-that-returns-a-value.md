---
title: "如何︰ 调用返回一个值 (Visual Basic 中) 的过程 |Microsoft 文档"
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
- procedure calls, returning values
- Visual Basic code, procedures
- procedures, calling
- procedures, returning a value
ms.assetid: a445127b-0f5f-465a-98fb-3e514b93d115
caps.latest.revision: 15
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
ms.openlocfilehash: df6bb1ed8acf5f86a290d67fec9c053cfe5245d2
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-a-procedure-that-returns-a-value-visual-basic"></a>如何：调用返回值的过程 (Visual Basic)
一个`Function`过程返回到调用代码的值。 它通过调用包括其名称和参数放在赋值语句或表达式中的右边。  
  
### <a name="to-call-a-function-procedure-within-an-expression"></a>若要调用表达式在 Function 过程  
  
1.  使用`Function`过程名称相同的方式使用变量。 您可以使用`Function`过程调用可以在表达式中使用变量或常量的任何位置。  
  
2.  过程名后面加上括号将参数列表括起来。 如果不有任何参数，可以选择省略括号。 但是，使用括号使代码易于阅读。  
  
3.  将参数放在括号内，用逗号分隔参数列表中。 请确保您的相同顺序的参数提供的`Function`过程定义对应的参数。  
  
     或者，您可以按名称传递一个或多个参数。 有关详细信息，请参阅[传递的参数按位置和名称](./passing-arguments-by-position-and-by-name.md)。  
  
4.  从过程返回的值参与只是作为值的表达式的变量或常数那样。  
  
### <a name="to-call-a-function-procedure-in-an-assignment-statement"></a>若要在赋值语句中调用 Function 过程  
  
1.  使用`Function`过程名称后面等号 (`=`) 登录赋值语句。  
  
2.  过程名后面加上括号将参数列表括起来。 如果不有任何参数，可以选择省略括号。 但是，使用括号使代码易于阅读。  
  
3.  将参数放在括号内，用逗号分隔参数列表中。 请确保您的相同顺序的参数提供的`Function`过程定义相应的参数，除非您按名称传递它们。  
  
4.  从过程返回的值存储在变量或赋值语句左侧的属性。  
  
## <a name="example"></a>示例  
 下面的示例调用[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]<xref:Microsoft.VisualBasic.Interaction.Environ%2A>来检索操作系统环境变量的值。</xref:Microsoft.VisualBasic.Interaction.Environ%2A> 第一个行调用`Environ`内使用表达式，并且第二个行调用它在赋值语句。 `Environ`将变量名称作为其唯一的参数。 它返回到调用代码的变量的值。  
  
 [!code-vb[VbVbcnProcedures #&7;](./codesnippet/VisualBasic/how-to-call-a-procedure-that-returns-a-value_1.vb)]  
  
## <a name="see-also"></a>请参见  
 [Function 过程](./function-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [如何︰ 创建返回一个值的过程](./how-to-create-a-procedure-that-returns-a-value.md)   
 [如何︰ 从过程返回值](./how-to-return-a-value-from-a-procedure.md)   
 [如何：调用不返回值的过程](./how-to-call-a-procedure-that-does-not-return-a-value.md)
