---
title: "如何︰ 调用重载的过程 (Visual Basic 中) |Microsoft 文档"
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
- procedures, overloading
- procedures, calling
- procedures, multiple versions
- procedure calls, overloaded
ms.assetid: 3bb331fb-f6bc-406f-9ca0-9609b497014c
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
ms.openlocfilehash: 0da83aa63bf013d841f2a01a535726f3b03497a1
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-an-overloaded-procedure-visual-basic"></a>如何：调用重载过程 (Visual Basic)
重载过程的优点是在调用更灵活。 调用代码可以获取传递给过程，然后调用单个过程名，无论它传递的哪些参数所需的信息。  
  
### <a name="to-call-a-procedure-that-has-more-than-one-version-defined"></a>若要调用具有定义的多个版本的过程  
  
1.  在调用代码中，确定要传递给过程的数据。  
  
2.  以正常方式表示的参数列表中的数据写入过程调用。 请确保参数匹配的参数列表中为过程定义的版本之一。  
  
3.  无需确定要调用的过程的哪个版本。 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将控制权传递给参数列表匹配的版本。  
  
     下面的示例调用`post`过程中声明[如何︰ 定义一个过程的多个版本](./how-to-define-multiple-versions-of-a-procedure.md)。 它会获取客户标识，确定它是否是`String`或`Integer`，然后在任一情况下调用相同的过程。  
  
     [!code-vb[VbVbcnProcedures #&56;](./codesnippet/VisualBasic/how-to-call-an-overloaded-procedure_1.vb)]  
  
     [!code-vb[VbVbcnProcedures #&57;](./codesnippet/VisualBasic/how-to-call-an-overloaded-procedure_2.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [过程重载](./procedure-overloading.md)   
 [故障排除过程](./troubleshooting-procedures.md)   
 [如何︰ 定义一个过程的多个版本](./how-to-define-multiple-versions-of-a-procedure.md)   
 [如何︰ 重载带有可选参数的过程](./how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [如何︰ 重载参数数量不确定的过程](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [重载过程注意事项](./considerations-in-overloading-procedures.md)   
 [重载决策](./overload-resolution.md)   
 [重载](../../../../visual-basic/language-reference/modifiers/overloads.md)
