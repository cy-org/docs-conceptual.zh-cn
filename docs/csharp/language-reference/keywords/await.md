---
title: "await（C# 参考）"
ms.date: 2017-05-22
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- await_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- await keyword [C#]
- await [C#]
ms.assetid: 50725c24-ac76-4ca7-bca1-dd57642ffedb
caps.latest.revision: 36
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 28be25d2f467ea5df4de50516bfa03347c77081e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="await-c-reference"></a>await（C# 参考）
`await` 运算符应用于异步方法中的任务，在方法的执行中插入挂起点，直到所等待的任务完成。 任务表示正在进行的工作。  
  
`await` 仅可用于由 [async](../../../csharp/language-reference/keywords/async.md) 关键字修改的异步方法中。 使用 `async` 修饰符定义并且通常包含一个或多个 `await` 表达式的这类方法称为异步方法。  
  
> [!NOTE]
>  `async` 和 `await` 关键字是在 C# 5 中引入的。 有关异步编程的说明，请参阅[使用 Async 和 Await 的异步编程](../../../csharp/programming-guide/concepts/async/index.md)。  
  
应用 `await` 运算符的任务通常由实现[基于任务的异步模式](../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)的方法调用返回。 包括返回 <xref:System.Threading.Tasks.Task>、<xref:System.Threading.Tasks.Task%601> 和 `System.Threading.Tasks.ValueType<TResult>` 对象的方法。  

  
 如下示例中，<xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A?displayProperty=fullName> 方法返回 `Task<byte[]>`。 当任务完成时，任务约定生成实际字节数组。 `await` 运算符挂起执行，直到 <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> 方法完成其操作。 同时，控制权会返回给 `GetPageSizeAsync` 的调用方。 任务结束执行时，`await` 表达式的计算结果为字节数组。  

[!code-cs[await-example](../../../../samples/snippets/csharp/language-reference/keywords/await/await1.cs)]  

> [!IMPORTANT]
>  有关完整示例，请参阅[演练：使用 async 和 await 访问 Web](../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)。 可以从 Microsoft 网站的[开发者代码示例](http://go.microsoft.com/fwlink/?LinkID=255191&clcid=0x409)中下载示例。 该示例处于 AsyncWalkthrough_HttpClient 项目中。  
  
如前一示例所示，如果 `await` 应用于返回 `Task<TResult>` 的方法调用的结果，则 `await` 表达式的类型为 `TResult`。 如果 `await` 应用于返回 `Task` 的方法调用的结果，则 `await` 表达式的类型为 `void`。 以下示例演示了差异。  
  
```csharp  
// await keyword used with a method that returns a Task<TResult>.  
TResult result = await AsyncMethodThatReturnsTaskTResult();  
  
// await keyword used with a method that returns a Task.  
await AsyncMethodThatReturnsTask();  

// await keyword used with a method that returns a ValueTask<TResult>.
TResult result = await AsyncMethodThatReturnsValueTaskTResult();
```  
  
`await` 表达式不阻止正在执行它的线程。 而是使编译器将剩下的异步方法注册为等待任务的延续任务。 控制权随后会返回给异步方法的调用方。 任务完成时，它会调用其延续任务，异步方法的执行会在暂停的位置处恢复。  
  
`await` 表达式只能在由 `async` 修饰符标记的封闭方法体、lambda 表达式或异步方法中出现。 术语 await 在该上下文中仅用作关键字。 在其他位置，它会解释为标识符。 在方法、Lambda 表达式或匿名方法中，`await` 表达式不能在同步函数体、查询表达式、[lock 语句](../../../csharp/language-reference/keywords/lock-statement.md)块或[不安全](../../../csharp/language-reference/keywords/unsafe.md)上下文中出现。  
  
## <a name="exceptions"></a>异常  
大多数异步方法返回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>。 返回任务的属性携带有关其状态和历史记录的信息，如任务是否完成、异步方法是否导致异常或已取消以及最终结果是什么。 `await` 运算符通过在由 `GetAwaiter` 方法返回的对象上调用方法来访问那些属性。  
  
如果等待的返回任务的异步方法会导致异常，则 `await` 运算符重新引发异常。  
  
如果等待的任务返回异步方法取消，则 `await` 运算符会重新引发 <xref:System.OperationCanceledException>。  
  
处于故障状态的单个任务可以反映多个异常。 例如，任务可能是对 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> 调用的结果。 等待此类任务时，等待操作仅重新引发异常之一。 但是，无法预测重新引发的异常。  
  
有关异步方法中的错误处理的示例，请参阅 [try catch](../../../csharp/language-reference/keywords/try-catch.md)。  
  
## <a name="example"></a>示例  
下面的示例返回页面（页面 URL 作为命令行参数传递给页面）中的字符总数。 此示例调用 `GetPageLengthsAsync` 方法，此方法标记有 `async` 关键字。 而 `GetPageLengthsAsync` 方法使用 `await` 关键字等待对 <xref:System.Net.Http.HttpClient.GetStringAsync%2A?displayProperty=fullName> 方法的调用。  

[!code-cs[await-example](../../../../samples/snippets/csharp/language-reference/keywords/await/await2.cs)]  

由于不支持在应用程序入口点中使用 `async` 和`await`，因此我们无法将 `async` 属性应用到 `Main` 方法，也无法等待 `GetPageLengthsAsync` 方法调用。 我们可通过检索 <xref:System.Threading.Tasks.Task%601.Result?displayProperty=fullName> 属性的值来确保 `Main` 方法等待异步操作完成。 对于不返回值的任务，可调用 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=fullName> 方法。 

## <a name="see-also"></a>另请参阅  
[使用 Async 和 Await 的异步编程](../../../csharp/programming-guide/concepts/async/index.md)   
[演练：使用 Async 和 Await 访问 Web](../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
[async](../../../csharp/language-reference/keywords/async.md)

