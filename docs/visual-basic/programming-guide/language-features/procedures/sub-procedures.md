---
title: "Sub 过程 (Visual Basic) |Microsoft 文档"
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
- Sub procedures, about Sub procedures
- statement blocks
- Sub procedures, calling
- procedures, calling
- Sub procedures, syntax
- Sub procedures
- procedures, Sub
- syntax, Sub procedures
ms.assetid: 6a0a4958-ed0a-4d3d-8d31-0772c82bda58
caps.latest.revision: 21
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
ms.openlocfilehash: d224fa3338ca707070ee431380578a8fdde47e07
ms.lasthandoff: 03/13/2017

---
# <a name="sub-procedures-visual-basic"></a>Sub 过程 (Visual Basic)
一个`Sub`过程是一系列[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]语句括`Sub`和`End Sub`语句。 `Sub`过程执行一项任务，然后将控件返回到调用代码中，但是它不到调用代码返回一个值。  
  
 每次调用该过程，其执行语句，开头的第一个可执行语句后`Sub`语句，并与第一个结束`End Sub`， `Exit Sub`，或`Return`遇到的语句。  
  
 您可以定义`Sub`模块、 类和结构中的过程。 默认情况下，它是`Public`，这意味着您可以调用它从任意位置的应用程序有权访问模块、 类或结构在其中定义中。 术语，*方法*，描述`Sub`或`Function`从外部其定义访问的过程模块、 类或结构。 有关详细信息，请参阅[过程](./index.md)。  
  
 一个`Sub`过程可以采用参数，如常量、 变量或表达式，通过调用代码传递给它。  
  
## <a name="declaration-syntax"></a>声明语法  
 声明的语法`Sub`过程是，如下所示︰  
  
 `[`*modifiers* `] Sub`*subname* `[(` *parameterlist*  `)]`  
  
 `' Statements of the Sub procedure.`  
  
 `End Sub`  
  
 `modifiers`可以指定访问级别和重载、 重写、 共享和隐藏有关的信息。 有关详细信息，请参阅[Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)。  
  
## <a name="parameter-declaration"></a>参数声明  
 声明类似于如何声明变量时，指定参数名称和数据类型的每个过程参数。 您还可以指定传递机制，并指示参数是可选或参数数组。  
  
 参数列表中每个参数的语法是，如下所示︰  
  
 `[Optional] [ByVal | ByRef] [ParamArray]`  *parametername*`As`*数据类型    *  
  
 如果该参数是可选的您还必须提供默认值作为其声明的一部分。 用于指定默认值的语法如下所示︰  
  
 `Optional [ByVal | ByRef]`  *parametername*`As`*datatype*`=`*默认值        *  
  
### <a name="parameters-as-local-variables"></a>作为本地变量的参数  
 当控制权传递给该过程时，每个参数被视为本地变量。 也就是说，它的生存期即相同过程，并且其作用域为整个过程。  
  
## <a name="calling-syntax"></a>调用语法  
 您可以调用`Sub`显式使用独立的调用语句的过程。 不能在表达式中使用其名称来调用它。 您必须提供值的所有参数，不是可选的并且必须将参数列表括在括号中。 如果未不提供任何参数，可以选择省略括号。 使用`Call`关键字是可选的但不是建议这样做。  
  
 对的调用语法`Sub`过程是，如下所示︰  
  
 `[Call]`  *子命名* `[(` *argumentlist*`)]`  
  
 您可以调用`Sub`从定义它的类之外的方法。 首先，您必须使用`New`关键字来创建类的实例，或调用一个方法返回类的实例。 有关详细信息，请参阅[New 运算符](../../../../visual-basic/language-reference/operators/new-operator.md)。 然后，使用以下语法来调用`Sub`实例对象的方法︰  
  
 *Object*.*methodname*`[(`*argumentlist*`)]`  
  
### <a name="illustration-of-declaration-and-call"></a>声明和调用的插图  
 以下`Sub`过程通知计算机操作员哪个任务应用程序即将执行，并且还显示时间戳。 而不是重复这段代码开头的每个任务，该应用程序只调用`tellOperator`从不同位置。 每次调用将一个字符串中的传递`task`标识开始执行的任务的参数。  
  
 [!code-vb[VbVbcnProcedures #&2;](./codesnippet/VisualBasic/sub-procedures_1.vb)]  
  
 下面的示例演示如何调用典型`tellOperator`。  
  
 [!code-vb[VbVbcnProcedures #&3;](./codesnippet/VisualBasic/sub-procedures_2.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [Function 过程](./function-procedures.md)   
 [属性过程](./property-procedures.md)   
 [运算符过程](./operator-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [如何︰ 调用不返回值的过程](./how-to-call-a-procedure-that-does-not-return-a-value.md)   
 [如何︰ 在 Visual Basic 中调用事件处理程序](./how-to-call-an-event-handler.md)
