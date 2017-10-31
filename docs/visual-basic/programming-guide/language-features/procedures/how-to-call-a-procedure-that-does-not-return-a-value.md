---
title: "如何︰ 调用不返回值 (Visual Basic 中) 的过程 |Microsoft 文档"
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
ms.assetid: 259b49a3-a3c1-4254-ba8c-73cdc4127703
caps.latest.revision: 17
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
ms.openlocfilehash: 17b2b902f3ee6ab79b2614b7742aa08fefab2420
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-a-procedure-that-does-not-return-a-value-visual-basic"></a>如何：调用不返回值的过程 (Visual Basic)
一个`Sub`过程不返回到调用代码的一个值。 显式调用该过程与独立的调用语句。 不能只需使用其名称在表达式中调用它。  
  
### <a name="to-call-a-sub-procedure"></a>若要调用 Sub 过程  
  
1.  指定的名称`Sub`过程。  
  
2.  过程名后面加上括号将参数列表括起来。 如果不有任何参数，可以选择省略括号。 但是，使用括号使代码易于阅读。  
  
3.  将参数放在括号内，用逗号分隔参数列表中。 请确保您的相同顺序的参数提供的`Sub`过程定义对应的参数。  
  
     下面的示例调用[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]<xref:Microsoft.VisualBasic.Interaction.AppActivate%2A>函数以激活应用程序窗口。</xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A>将窗口标题作为其唯一的参数。</xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> 不返回到调用代码的一个值。 如果未运行记事本过程，本示例将引发<xref:System.ArgumentException>。</xref:System.ArgumentException> `Shell`过程假定应用程序是否在指定的路径。  
  
     [!code-vb[VbVbalrCatRef #&11;](./codesnippet/VisualBasic/how-to-call-a-procedure-that-does-not-return-a-value_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.Interaction.Shell%2A></xref:Microsoft.VisualBasic.Interaction.Shell%2A>   
 <xref:System.ArgumentException></xref:System.ArgumentException>   
 [过程](./index.md)   
 [Sub 过程](./sub-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [如何︰ 创建过程](./how-to-create-a-procedure.md)   
 [如何︰ 调用返回一个值的过程](./how-to-call-a-procedure-that-returns-a-value.md)   
 [如何︰ 在 Visual Basic 中调用事件处理程序](./how-to-call-an-event-handler.md)
