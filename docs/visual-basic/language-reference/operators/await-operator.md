---
title: "Await 运算符 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Await
helpviewer_keywords:
- Await operator [Visual Basic]
- Await [Visual Basic]
ms.assetid: 6b1ce283-e92b-4ba7-b081-7be7b3d37af9
caps.latest.revision: 30
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: b50b9c7283ddd4d3f8484854bdffff3d76181c9f
ms.lasthandoff: 03/13/2017

---
# <a name="await-operator-visual-basic"></a>Await 运算符 (Visual Basic)
在异步方法或 lambda 表达式中对操作数应用 `Await` 运算符可暂停执行方法，直到所等待的任务完成。 任务表示正在进行的工作。  
  
 在其中方法`Await`使用必须具有[异步](../../../visual-basic/language-reference/modifiers/async.md)修饰符。 此类定义的方法，通过使用`Async`修饰符，并通常包含一个或多`Await`表达式中，称为*async 方法*。  
  
> [!NOTE]
>  `Async` 和 `Await` 关键字是在 Visual Studio 2012 中引入的。 有关异步编程的介绍，请参阅[使用 Async 和 Await 的异步编程](../../../visual-basic/programming-guide/concepts/async/index.md)。  
  
 通常情况下，您将应用该任务`Await`运算符是通过实现的方法调用的返回值[基于任务的异步模式](http://go.microsoft.com/fwlink/?LinkId=204847)，也就是说，一个<xref:System.Threading.Tasks.Task>或一种<xref:System.Threading.Tasks.Task%601>。</xref:System.Threading.Tasks.Task%601> </xref:System.Threading.Tasks.Task>  
  
 在下面的代码中，<xref:System.Net.Http.HttpClient>方法<xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A>返回`getContentsTask`、 `Task(Of Byte())`。</xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> </xref:System.Net.Http.HttpClient> 当操作完成时，任务约定生成一个实际字节数组。 `Await` 运算符应用于 `getContentsTask` 以在 `SumPageSizesAsync` 中挂起执行，直到 `getContentsTask` 完成。 同时，控制权会返回给 `SumPageSizesAsync` 的调用方。 当 `getContentsTask` 完成之后，`Await` 表达式计算为字节数组。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
> [!IMPORTANT]
>  有关完整示例，请参阅[演练︰ 访问通过使用 Async 和 Await Web](../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)。 你可以下载示例从[开发人员代码示例](http://go.microsoft.com/fwlink/?LinkID=255191&clcid=0x409)Microsoft 网站上。 该示例处于 AsyncWalkthrough_HttpClient 项目中。  
  
 如果 `Await` 应用于返回 `Task(Of TResult)` 的方法调用结果，则 `Await` 表达式的类型为 TResult。 如果 `Await` 应用于返回 `Task` 的方法调用结果，则 `Await` 表达式不返回值。 以下示例演示了差异。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 `Await` 表达式或声明不阻止正在执行它的线程。 而是导致编译器在 `Await` 表达式之后，将剩下的异步方法注册为等待任务的后续部分。 控制权随后会返回给异步方法的调用方。 任务完成时，它会调用其延续任务，异步方法的执行会在暂停的位置处恢复。  
  
 `Await` 表达式只出现在由 `Async` 修饰符标记的一个立即封闭方法体或 lambda 表达式中。 术语*Await*用作关键字仅在该上下文中。 在其他位置，它会解释为标识符。 在异步方法或 lambda 表达式中，`Await`表达式中不能出现在查询表达式中，`catch`或`finally`块[重试...Catch...最后](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)中的循环控制变量表达式语句`For`或`For Each`循环中，或在正文中[SyncLock](../../../visual-basic/language-reference/statements/synclock-statement.md)语句。  
  
## <a name="exceptions"></a>异常  
 大多数异步方法返回<xref:System.Threading.Tasks.Task>或<xref:System.Threading.Tasks.Task%601>.</xref:System.Threading.Tasks.Task%601> </xref:System.Threading.Tasks.Task> 返回任务的属性携带有关其状态和历史记录的信息，如任务是否完成、异步方法是否导致异常或已取消以及最终结果是什么。 `Await` 运算符可访问这些属性。  
  
 如果等待的任务返回异步方法导致异常，则 `Await` 运算符会重新引发异常。  
  
 如果等待的返回任务的异步方法取消，`Await`运算符将重新引发<xref:System.OperationCanceledException>。</xref:System.OperationCanceledException>  
  
 处于故障状态的单个任务可以反映多个异常。  例如，任务可能是到<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>。</xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>调用的结果 等待此类任务时，等待操作仅重新引发异常之一。 但是，无法预测重新引发的异常。  
  
 异步方法中的错误处理的示例，请参阅[重试...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
## <a name="example"></a>示例  
 下面的 Windows 窗体示例阐释如何在异步方法 `WaitAsynchronouslyAsync` 中使用 `Await`。 将该方法的行为与 `WaitSynchronously` 的行为进行对比。 而无需`Await`运算符，`WaitSynchronously`会同步运行，不管是否使用`Async`修饰符在其定义和调用<xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName>在其主体中。</xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName>  
  
```vb  
Private Async Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
    ' Call the method that runs asynchronously.  
    Dim result As String = Await WaitAsynchronouslyAsync()  
  
    ' Call the method that runs synchronously.  
    'Dim result As String = Await WaitSynchronously()  
  
    ' Display the result.  
    TextBox1.Text &= result  
End Sub  
  
' The following method runs asynchronously. The UI thread is not  
' blocked during the delay. You can move or resize the Form1 window   
' while Task.Delay is running.  
Public Async Function WaitAsynchronouslyAsync() As Task(Of String)  
    Await Task.Delay(10000)  
    Return "Finished"  
End Function  
  
' The following method runs synchronously, despite the use of Async.  
' You cannot move or resize the Form1 window while Thread.Sleep  
' is running because the UI thread is blocked.  
Public Async Function WaitSynchronously() As Task(Of String)  
    ' Import System.Threading for the Sleep method.  
    Thread.Sleep(10000)  
    Return "Finished"  
End Function  
```  
  
## <a name="see-also"></a>另请参阅  
 [异步编程使用 Async 和 Await](../../../visual-basic/programming-guide/concepts/async/index.md)   
 [演练︰ 访问 Web 使用 Async 和 Await](../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [Async](../../../visual-basic/language-reference/modifiers/async.md)
