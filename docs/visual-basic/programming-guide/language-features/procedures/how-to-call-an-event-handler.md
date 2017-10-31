---
title: "如何︰ 在 Visual Basic 中调用事件处理程序 |Microsoft 文档"
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
- event handlers, calling
- event handlers
- procedures, event handlers
- procedures, calling
ms.assetid: 72e18ef8-144e-40df-a1f4-066a57271e28
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
ms.openlocfilehash: c5b300feca3415d1283d24179795a4ae92c61e52
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-an-event-handler-in-visual-basic"></a>如何：在 Visual Basic 中调用事件处理程序
*事件*的操作或匹配项 — 如鼠标单击或信用额度超出 —，识别，被某程序组件，并且为其编写代码进行响应。 *事件处理程序*是为响应某个事件而编写的代码。  
  
 中的事件处理程序[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]是`Sub`过程。 但是，您不能正常情况下调用此相同方式其他`Sub`过程。 相反，作为事件处理程序标识过程。 您可以执行此操作与[处理](../../../../visual-basic/language-reference/statements/handles-clause.md)子句和一个[WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md)变量，或使用[AddHandler 语句](../../../../visual-basic/language-reference/statements/addhandler-statement.md)。 使用`Handles`子句是声明中的事件处理程序的默认方式[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。 这是您在集成的开发环境 (IDE) 中进行编程时，事件处理程序会写入设计器的方法。 `AddHandler`语句是适用于在运行时动态地引发事件。  
  
 发生事件时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]自动调用事件处理程序。 有权访问该事件的任何代码会使它通过执行[RaiseEvent 语句](../../../../visual-basic/language-reference/statements/raiseevent-statement.md)。  
  
 可以将多个事件处理程序与同一个事件关联。 在某些情况下您可以从事件处理程序解除关联。 有关详细信息，请参阅[事件](../../../../visual-basic/programming-guide/language-features/events/index.md)。  
  
### <a name="to-call-an-event-handler-using-handles-and-withevents"></a>若要调用事件处理程序使用句柄和 WithEvents  
  
1.  请确保用声明了事件[Event 语句](../../../../visual-basic/language-reference/statements/event-statement.md)。  
  
2.  声明对象变量在模块或类级别，而使用[WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md)关键字。 `As`此变量的子句必须指定引发事件的类。  
  
3.  在处理事件的声明中`Sub`的过程中，添加[处理](../../../../visual-basic/language-reference/statements/handles-clause.md)子句，以指定`WithEvents`变量和事件名称。  
  
4.  发生事件时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]自动调用`Sub`过程。 你的代码可以使用`RaiseEvent`语句来引发事件。  
  
     下面的示例定义一个事件和一个`WithEvents`指的是引发该事件的类中的变量。 事件处理`Sub`过程使用`Handles`子句，以指定的类和它处理的事件。  
  
     [!code-vb[VbVbcnProcedures #&4;](./codesnippet/VisualBasic/how-to-call-an-event-handler_1.vb)]  
  
### <a name="to-call-an-event-handler-using-addhandler"></a>若要调用 AddHandler 使用事件处理程序  
  
1.  请确保用声明了事件`Event`语句。  
  
2.  执行[AddHandler 语句](../../../../visual-basic/language-reference/statements/addhandler-statement.md)以动态连接处理事件的`Sub`与该事件的过程。  
  
3.  发生事件时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]自动调用`Sub`过程。 你的代码可以使用`RaiseEvent`语句来引发事件。  
  
     下面的示例定义`Sub`过程来处理<xref:System.Windows.Forms.Form.Closing>窗体的事件。</xref:System.Windows.Forms.Form.Closing> 然后，它使用[AddHandler 语句](../../../../visual-basic/language-reference/statements/addhandler-statement.md)关联`catchClose` <xref:System.Windows.Forms.Form.Closing>。</xref:System.Windows.Forms.Form.Closing>一个事件处理程序的过程  
  
     [!code-vb[VbVbcnProcedures #&5;](./codesnippet/VisualBasic/how-to-call-an-event-handler_2.vb)]  
  
     可以通过执行取消事件处理程序从事件[RemoveHandler 语句](../../../../visual-basic/language-reference/statements/removehandler-statement.md)。  
  
## <a name="see-also"></a>请参见  
 [过程](./index.md)   
 [Sub 过程](./sub-procedures.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [AddressOf 运算符](../../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [如何︰ 创建过程](./how-to-create-a-procedure.md)   
 [如何：调用不返回值的过程](./how-to-call-a-procedure-that-does-not-return-a-value.md)
