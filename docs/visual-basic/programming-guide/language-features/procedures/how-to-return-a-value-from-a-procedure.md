---
title: "如何︰ 从过程 (Visual Basic 中) 返回一个值 |Microsoft 文档"
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
- Visual Basic code, procedures
- procedures, returning from
- procedures, returning a value
ms.assetid: 4bcc4724-2b4e-4df8-9b4b-16054607f87d
caps.latest.revision: 12
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
ms.openlocfilehash: 98f0fb0740a021a16e87454bfaebbfad7858477c
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-return-a-value-from-a-procedure-visual-basic"></a>如何：从过程返回值 (Visual Basic)
一个`Function`过程将值返回到调用代码可以通过执行`Return`语句或在遇到`Exit Function`或`End Function`语句。  
  
### <a name="to-return-a-value-using-the-return-statement"></a>返回值使用 Return 语句  
  
1.  放置`Return`语句完成该过程的任务时的时刻。  
  
2.  请按照`Return`想要返回到调用代码会生成值的表达式的关键字。  
  
3.  您可以有多个`Return`相同的过程中的语句。  
  
     以下`Function`过程计算的最长边或斜边直角三角形，并将其返回给调用代码。  
  
     [!code-vb[VbVbcnProcedures #&1;](./codesnippet/VisualBasic/how-to-return-a-value-from-a-procedure_1.vb)]  
  
     下面的示例演示如何调用典型`hypotenuse`，它用于存储返回的值。  
  
     [!code-vb[VbVbcnProcedures #&6;](./codesnippet/VisualBasic/how-to-return-a-value-from-a-procedure_2.vb)]  
  
### <a name="to-return-a-value-using-exit-function-or-end-function"></a>返回值使用退出函数或结束函数  
  
1.  在至少一个就地`Function`的过程中，赋值为该过程的名称。  
  
2.  当您执行`Exit Function`或`End Function`语句，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]返回最近分配给过程的名称的值。  
  
3.  您可以有多个`Exit Function`中的语句相同的过程，以及您可以混合使用`Return`和`Exit Function`相同的过程中的语句。  
  
4.  只能有一个`End Function`中的语句`Function`过程。  
  
     有关详细信息和示例，请参阅"返回值" [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)。  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [Sub 过程](./sub-procedures.md)   
 [属性过程](./property-procedures.md)   
 [运算符过程](./operator-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Return 语句](../../../../visual-basic/language-reference/statements/return-statement.md)   
 [如何︰ 创建返回一个值的过程](./how-to-create-a-procedure-that-returns-a-value.md)   
 [如何：调用返回值的过程](./how-to-call-a-procedure-that-returns-a-value.md)
