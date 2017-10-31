---
title: "递归过程 (Visual Basic 中) |Microsoft 文档"
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
- procedures, that call themselves
- procedures, recursive
- procedures, calling
- recursive procedures
- functions [Visual Basic], calling recursively
- recursion
ms.assetid: ba1d3962-b4c3-48d3-875e-96fdb4198327
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
ms.openlocfilehash: 9fc95cd5f7cfd5637f6282c6ef571eb81bac1816
ms.lasthandoff: 03/13/2017

---
# <a name="recursive-procedures-visual-basic"></a>递归过程 (Visual Basic)
一个*递归*过程是指调用自身。 一般情况下，这不是最有效的方法来编写[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]代码。  
  
 下面的过程使用递归来计算其原始参数的阶乘。  
  
 [!code-vb[VbVbcnProcedures #&51;](./codesnippet/VisualBasic/recursive-procedures_1.vb)]  
  
## <a name="considerations-with-recursive-procedures"></a>递归过程方面的注意事项  
 **限制条件**。 您必须在设计递归过程以测试可以终止此递归的至少一个条件和还必须处理任何此类条件均在合理数量的递归调用这种情况。 没有可以满足而不会出现的至少一个条件，您的过程运行高风险的在无限循环中执行。  
  
 **内存使用量**。 将应用程序将有限的数量的空间用于本地变量。 过程调用其本身，每次都会占用更多空间的其他副本的本地变量。 如果此过程持续下去，最终会导致<xref:System.StackOverflowException>错误。</xref:System.StackOverflowException>  
  
 **效率**。 您几乎总是可以替换为递归循环。 一个循环并没有初始化附加存储空间和返回值传递参数的系统开销。 您的性能可以大幅提高递归调用。  
  
 **相互递归**。 如果两个过程调用对方，可能会发现性能非常差或甚至产生无限循环。 此类设计提出一个递归过程中，与相同的问题，但很难检测和调试。  
  
 **调用时使用括号**。 当`Function`过程调用其自身以递归方式，您必须过程名后面加上括号，即使没有参数列表。 否则，执行的函数名称作为表示该函数的返回值。  
  
 **测试**。 如果您编写的递归过程，您应该测试它应非常小心以确保它总是能满足某些限制条件。 您还应确保您不能运行由于递归调用过多的内存不足。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.StackOverflowException></xref:System.StackOverflowException>   
 [过程](./index.md)   
 [Sub 过程](./sub-procedures.md)   
 [Function 过程](./function-procedures.md)   
 [属性过程](./property-procedures.md)   
 [运算符过程](./operator-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [过程重载](./procedure-overloading.md)   
 [故障排除过程](./troubleshooting-procedures.md)   
 [循环结构](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [异常疑难解答：System.StackOverflowException](http://msdn.microsoft.com/library/51b71217-c507-4f5b-bc35-0236180d7968)
