---
title: "重试...Catch...Finally 语句 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Try...Catch...Finally
- vb.when
- vb.Finally
- vb.Catch
- vb.Try
dev_langs:
- VB
helpviewer_keywords:
- Try...Catch...Finally statements
- Try statement
- try-catch exception handling, Try...Catch...Finally statements
- error handling, while running code
- Try statement, Try...Catch...Finally
- Finally keyword [Visual Basic], Try...Catch...Finally
- Catch statement
- When keyword
- Visual Basic code, handling errors while running
- structured exception handling, Try...Catch...Finally statements
ms.assetid: d6488026-ccb3-42b8-a810-0d97b9d6472b
caps.latest.revision: 69
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
ms.openlocfilehash: 379359e3a338746ccd440dbe1ad58c483e562dbe
ms.lasthandoff: 03/13/2017

---
# <a name="trycatchfinally-statement-visual-basic"></a>Try...Catch...Finally 语句 (Visual Basic)
提供了一种方法来处理时可能会发生在给定块中的代码中，仍在运行代码的部分或全部可能错误。  
  
## <a name="syntax"></a>语法  
  
```  
Try  
    [ tryStatements ]  
    [ Exit Try ]  
[ Catch [ exception [ As type ] ] [ When expression ]  
    [ catchStatements ]  
    [ Exit Try ] ]  
[ Catch ... ]  
[ Finally  
    [ finallyStatements ] ]  
End Try  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`tryStatements`|可选。 可能发生错误的语句。 可以是复合语句。|  
|`Catch`|可选。 多个`Catch`允许的块。 如果在处理时，则会发生异常`Try`阻止时，每个`Catch`文本顺序来确定是否将它与处理该异常，检查语句`exception`表示已引发的异常。|  
|`exception`|可选。 任何变量名称。 `exception` 的初始值是引发的错误的值。 与使用`Catch`指定错误捕获。 如果省略，`Catch`语句将捕获所有异常。|  
|`type`|可选。 指定类筛选器的类型。 如果值`exception`属于指定的类型`type`或派生类型的标识符将成为绑定到的异常对象。|  
|`When`|可选。 一个`Catch`语句`When`子句将捕获异常时，才`expression`的计算结果为`True`。 一个`When`子句只在检查的类型的异常之后, 应用和`expression`可能引用表示异常的标识符。|  
|`expression`|可选。 必须是隐式转换为`Boolean`。 描述泛型的筛选器的任何表达式。 通常用于筛选的错误号。 与使用`When`关键字来指定捕获错误时的情况。|  
|`catchStatements`|可选。 语句来处理在关联中发生的错误`Try`块。 可以是复合语句。|  
|`Exit Try`|可选。 跳出关键字`Try...Catch...Finally`结构。 紧随的代码处继续执行`End Try`语句。 `Finally`仍将继续执行语句。 中不允许使用`Finally`块。|  
|`Finally`|可选。 一个`Finally`当执行离开的任何部分，则始终执行块`Try...Catch`语句。|  
|`finallyStatements`|可选。 所有其他错误处理发生后执行的语句。|  
|`End Try`|终止`Try...Catch...Finally`结构。|  
  
## <a name="remarks"></a>备注  
 如果希望特定异常可能会出现在特定的代码部分的过程，请将代码放入`Try`块又使用`Catch`块来保留控制处理该异常发生时。  
  
 一个`Try…Catch`语句组成`Try`块后跟一个或多个`Catch`子句，指定的各种异常处理程序。 引发异常时`Try`块中，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]寻找`Catch`处理该异常的语句。 如果匹配`Catch`找不到语句，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]检查调用当前方法，然后会遍历调用堆栈的方法。 如果不是`Catch`找到该块，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]向用户显示一条未处理的异常消息并停止执行该程序。  
  
 您可以使用多个`Catch`中的语句`Try…Catch`语句。 如果执行此操作的顺序`Catch`子句很重要，因为它们会按顺序检查。 在使用更笼统的子句之前获取特定性更强的异常。  
  
 以下`Catch`语句条件将具体性，并将捕获所有异常派生自<xref:System.Exception>类。</xref:System.Exception> 通常应作为上一次将这些变体之一`Catch`阻止入`Try...Catch...Finally`后捕获您期望的所有特定异常的结构。 控制流可以永远不能到达`Catch`遵循以下任一这些变体的块。  
  
-   `type`是`Exception`，例如︰`Catch ex As Exception`  
  
-   该语句没有`exception`变量，例如︰`Catch`  
  
 当`Try…Catch…Finally`语句嵌套在另一个`Try`块中，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]首先检查每个`Catch`语句中使用最内层`Try`块。 如果没有匹配`Catch`找到语句，则继续搜索`Catch`语句的外部`Try…Catch…Finally`块。  
  
 从本地变量`Try`块中均不提供`Catch`进行阻止，因为它们是单独的块。 如果您想要在多个块中使用变量，之外声明该变量`Try...Catch...Finally`结构。  
  
> [!TIP]
>  `Try…Catch…Finally`语句是可用作 IntelliSense 代码段。 在代码段管理器中，展开**代码模式-如果，对于每个，Try Catch 属性，等**，然后**错误处理 （异常）**。 有关详细信息，请参阅[代码片段](https://docs.microsoft.com/visualstudio/ide/code-snippets)。  
  
## <a name="finally-block"></a>Finally 块  
 如果您有一个或多个语句在退出之前必须运行`Try`结构，请使用`Finally`块。 控制权将传递给`Finally`阻止它传递出之前`Try…Catch`结构。 即使内任何位置发生异常，这是如此`Try`结构。  
  
 一个`Finally`块可用于运行任何代码必须执行，即使出现异常。 控制权将传递给`Finally`块而不考虑如何`Try...Catch`阻止退出。  
  
 中的代码`Finally`阻止运行，即使您的代码遇到`Return`中的语句`Try`或`Catch`块。 控件未通过从`Try`或`Catch`阻止对相应`Finally`阻止在以下情况︰  
  
-   [End 语句](../../../visual-basic/language-reference/statements/end-statement.md)中遇到`Try`或`Catch`块。  
  
-   一个<xref:System.StackOverflowException>中引发`Try`或`Catch`块。</xref:System.StackOverflowException>  
  
 不能用来显式将执行传输到`Finally`块。 将执行共转`Finally`块不是有效的除非通过异常。  
  
 如果`Try`语句未包含至少一个`Catch`块中，它必须包含`Finally`块。  
  
> [!TIP]
>  如果不需要捕获特定异常，`Using`语句的行为类似`Try…Finally`块中，且保证会处置的资源，而不考虑如何退出块。 这是即使使用未经处理的异常，则返回 true。 有关详细信息，请参阅[Using 语句](../../../visual-basic/language-reference/statements/using-statement.md)。  
  
## <a name="exception-argument"></a>异常参数  
 `Catch`块`exception`参数是实例<xref:System.Exception>类或派生自类`Exception`类</xref:System.Exception> `Exception`类实例对应于中出现的错误`Try`块。  
  
 属性的`Exception`对象帮助以确定原因和处理的异常的位置。 例如，<xref:System.Exception.StackTrace%2A>属性列出导致异常，帮助您找到代码中发生错误的调用的方法。</xref:System.Exception.StackTrace%2A> <xref:System.Exception.Message%2A>返回一条描述异常的消息。</xref:System.Exception.Message%2A> <xref:System.Exception.HelpLink%2A>返回指向相关联的帮助文件的链接。</xref:System.Exception.HelpLink%2A> <xref:System.Exception.InnerException%2A>返回`Exception`导致当前异常，或它的对象返回`Nothing`如果没有原始`Exception`。</xref:System.Exception.InnerException%2A>  
  
## <a name="considerations-when-using-a-trycatch-statement"></a>使用一试时的注意事项...Catch 语句  
 使用`Try…Catch`语句只是为了发出信号不寻常或意外程序事件的发生次数。 此问题的原因包括︰  
  
-   在运行时捕获的异常创建额外系统开销，并可能需要比预检查以避免异常慢。  
  
-   如果`Catch`块不能正确处理，该异常可能不会正确报告给用户。  
  
-   异常处理会使程序更复杂。  
  
 您并不总是需要`Try…Catch`语句，以检查可能会发生事件的条件。 以下示例检查文件是否存在便会尝试将其打开。 这减少了用于捕获引发的异常需要<xref:System.IO.File.OpenText%2A>方法。</xref:System.IO.File.OpenText%2A>  
  
 [!code-vb[VbVbalrStatements #&94;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_1.vb)]  
  
 确保在该代码`Catch`块可以将异常正确报告给用户，无论是通过线程安全日志记录还是相应的消息。 否则，异常可能仍是未知的。  
  
## <a name="async-methods"></a>异步方法  
 如果将标记的方法，其[异步](../../../visual-basic/language-reference/modifiers/async.md)修饰符，您可以使用[Await](../../../visual-basic/language-reference/operators/await-operator.md)方法中的运算符。 具有的语句`Await`运算符暂停执行方法，直到所等待的任务完成。 任务表示正在进行的工作。 当与相关联的任务`Await`运算符完成后，执行将继续在同一方法中。 有关详细信息，请参阅[异步程序中的控制流](../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md)。  
  
 任务返回的异步方法最终可能处于错误状态，指示它完成由于未经处理的异常。 一项任务可能还会已取消状态，这会导致`OperationCanceledException`引发外 await 表达式。 若要捕获其中任何一种异常，将放置`Await`中的任务相关联的表达式`Try`块，并捕获该异常在`Catch`块。 在本主题后面提供了示例。  
  
 一项任务可能处于错误状态，因为多个异常的负责其处理故障。 例如，任务可能是到<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>。</xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>调用的结果 当等待此任务时，捕获的异常都只有一个例外，而您无法预测将捕获的异常。 在本主题后面提供了示例。  
  
 `Await`表达式不能包含在内`Catch`块或`Finally`块。  
  
## <a name="iterators"></a>迭代器  
 迭代器函数或`Get`访问器在集合上执行自定义的迭代。 迭代器使用[产生](../../../visual-basic/language-reference/statements/yield-statement.md)语句可返回一次该集合的每个元素。 通过使用调用迭代器函数[为每个...下一条语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)。  
  
 一个`Yield`语句可以是内部`Try`块。 一个`Try`包含块`Yield`语句可以有`Catch`阻止，并且也能`Finally`块。 请参阅的"重试块在 Visual Basic"部分[迭代器](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7)有关的示例。  
  
 一个`Yield`语句不能包含在内`Catch`块或`Finally`块。  
  
 如果`For Each`主体 （在之外的迭代器函数） 引发了异常，`Catch`未执行迭代器函数中的块，但`Finally`执行迭代器函数中的块。 一个`Catch`迭代器函数内部的块将捕获在迭代器函数内部发生的异常。  
  
## <a name="partial-trust-situations"></a>部分信任的情况下  
 在部分信任情况下，例如在网络共享上托管的应用程序`Try...Catch...Finally`不捕获调用包含调用该方法之前发生的安全异常。 以下示例中，则将其置于服务器共享并运行在这里时, 产生错误"System.Security.SecurityException︰ 请求失败。" 有关安全异常的详细信息，请参阅<xref:System.Security.SecurityException>类。</xref:System.Security.SecurityException>  
  
 [!code-vb[VbVbalrStatements #&85;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_2.vb)]  
  
 在此类的部分信任情况下，您必须将`Process.Start`位于一个单独的语句`Sub`。 首次调用`Sub`将失败。 这使`Try...Catch`可以捕捉到它之前`Sub`，其中包含`Process.Start`已启动并产生安全异常。  
  
## <a name="example"></a>示例  
 下面的示例演示的结构`Try...Catch...Finally`语句。  
  
 [!code-vb[VbVbalrStatements #&86;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_3.vb)]  
  
## <a name="example"></a>示例  
 在下面的示例中，`CreateException`方法抛出异常`NullReferenceException`。 生成异常的代码不在`Try`块。 因此，`CreateException`方法未处理异常。 `RunSample`方法未处理该异常，因为调用`CreateException`方法正在`Try`块。  
  
 该示例包括`Catch`语句的几种例外情况之外，按从最特定到最常见。  
  
 [!code-vb[VbVbalrStatements #&91;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_4.vb)]  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用`Catch When`语句筛选条件表达式。 如果条件表达式的计算结果为`True`中的代码`Catch`块将运行。  
  
 [!code-vb[VbVbalrStatements #&92;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_5.vb)]  
  
## <a name="example"></a>示例  
 下面的示例有`Try…Catch`中包含的语句`Try`块。 内部`Catch`块中引发异常有其`InnerException`属性设置为原始异常。 外部`Catch`块都会报告自己的异常和内部异常。  
  
 [!code-vb[VbVbalrStatements #&93;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_6.vb)]  
  
## <a name="example"></a>示例  
 下面的示例阐释异步方法的异常处理。 若要捕获的异常，适用于异步任务，`Await`表达式是在`Try`的调用方和异常块中捕捉到`Catch`块。  
  
 在示例中取消注释 `Throw New Exception` 行以演示异常处理。 中捕获到异常`Catch`阻止时，该任务的`IsFaulted`属性设置为`True`，任务的`Exception.InnerException`属性设置为异常。  
  
 取消注释`Throw New OperationCancelledException`行以演示当您取消异步过程中会发生什么情况。 中捕获到异常`Catch`块和任务的`IsCanceled`属性设置为`True`。 但是，在不能应用于此示例中，某些情况下`IsFaulted`设置为`True`和`IsCanceled`设置为`False`。  
  
 [!code-vb[csAsyncExceptions&#1;](../../../csharp/language-reference/keywords/codesnippet/VisualBasic/try-catch-finally-statement_7.vb)]  
  
## <a name="example"></a>示例  
 下面的示例阐释了在多个任务可能导致多个异常的情况中的异常处理。 `Try`块都有`Await`任务的表达式，<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>返回。</xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> 当这三项任务的任务已完成<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>应用都已完成。</xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>  
  
 三个任务中的每一个都会导致异常。 `Catch`块循环访问异常，它位于`Exception.InnerExceptions`任务的属性，`Task.WhenAll`返回。  
  
 [!code-vb[csAsyncExceptions&#3;](../../../csharp/language-reference/keywords/codesnippet/VisualBasic/try-catch-finally-statement_8.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.Information.Err%2A></xref:Microsoft.VisualBasic.Information.Err%2A>   
 <xref:System.Exception></xref:System.Exception>   
 [Exit 语句](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [On Error 语句](../../../visual-basic/language-reference/statements/on-error-statement.md)   
 [使用代码段的最佳实践](https://docs.microsoft.com/visualstudio/ide/best-practices-for-using-code-snippets)   
 [异常处理](https://msdn.microsoft.com/library/dd997415)   
 [Throw 语句](../../../visual-basic/language-reference/statements/throw-statement.md)
