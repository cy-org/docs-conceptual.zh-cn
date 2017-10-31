---
title: "异步返回类型 (C#)"
ms.custom: 
ms.date: 2075-05-29
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: ddb2539c-c898-48c1-ad92-245e4a996df8
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9e7f31d4160d44668f4ddea5e1ca0eaa3037c5a5
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="async-return-types-c"></a>异步返回类型 (C#)
异步方法可以具有以下返回类型：

- <xref:System.Threading.Tasks.Task%601>（对于返回值的异步方法）。 
 
-  <xref:System.Threading.Tasks.Task>（对于执行操作但不返回任何值的异步方法）。

- `void`（对于事件处理程序）。 

- 从 C# 7 开始，任何具有可访问的 `GetAwaiter` 方法的类型。 `GetAwaiter` 方法返回的对象必须实现 <xref:System.Runtime.CompilerServices.ICriticalNotifyCompletion?displayProperty=fullName> 接口。
  
有关异步方法的详细信息，请参阅[使用 Async 和 Await 的异步编程 (C#)](../../../../csharp/programming-guide/concepts/async/index.md)。  
  
在以下其中一节检查每个返回类型，且在本主题末尾可以找到使用全部三种类型的完整示例。  
  
##  <a name="BKMK_TaskTReturnType"></a>Task(T) 返回类型  
<xref:System.Threading.Tasks.Task%601> 返回类型用于某种异步方法，此异步方法包含 [return](../../../../csharp/language-reference/keywords/return.md) (C#) 语句，其中操作数具有类型 `TResult`。  
  
在下面的示例中，`GetLeisureHours` 异步方法包含返回整数的 `return` 语句。 因此，该方法声明必须指定 `Task<int>` 的返回类型。  <xref:System.Threading.Tasks.Task.FromResult%2A> 异步方法是返回字符串的操作的占位符。
  
[!code-cs[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns1.cs)]

在 `ShowTodaysInfo` 方法中从 await 表达式内调用 `GetLeisureHours` 时，await 表达式检索存储在由 `GetLeisureHours` 方法返回的任务中的整数值（`leisureHours` 的值）。 有关 await 表达式的详细信息，请参阅 [await](../../../../csharp/language-reference/keywords/await.md)。  
  
通过从应用程序 `await` 中分离对 `GetLeisureHours` 的调用，你可以更好地了解此操作，如下面的代码所示。 对非立即等待的方法 `TaskOfT_MethodAsync` 的调用返回 `Task<int>`，正如你从方法声明预料的一样。 该任务指派给示例中的 `integerTask` 变量。 因为 `integerTask` 是 <xref:System.Threading.Tasks.Task%601>，所以它包含类型 `TResult` 的 <xref:System.Threading.Tasks.Task%601.Result> 属性。 在这种情况下，TResult 表示整数类型。 `await` 应用于 `integerTask`，await 表达式的计算结果为 `integerTask` 的 <xref:System.Threading.Tasks.Task%601.Result%2A> 属性内容。 此值分配给 `result2` 变量。  
  
> [!IMPORTANT]
>  <xref:System.Threading.Tasks.Task%601.Result%2A> 属性为阻止属性。 如果你在其任务完成之前尝试访问它，当前处于活动状态的线程将被阻止，直到任务完成且值为可用。 在大多数情况下，应通过使用 `await` 访问此值，而不是直接访问属性。 <br/> 上一示例通过检索 <xref:System.Threading.Tasks.Task%601.Result%2A> 属性的值来阻止主线程，从而使 `ShowTodaysInfo` 方法可在应用程序结束之前完成执行。  

[!code-cs[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns1a.cs#1)]
  
##  <a name="BKMK_TaskReturnType"></a>任务返回类型  
不包含 `return` 语句的异步方法或包含不返回操作数的 `return` 语句的异步方法通常具有返回类型 <xref:System.Threading.Tasks.Task>。 如果此类方法同步运行，它们将返回 `void`。 如果在异步方法中使用 <xref:System.Threading.Tasks.Task> 返回类型，调用方法可以使用 `await` 运算符暂停调用方的完成，直至被调用的异步方法结束。  
  
如下示例中，`WaitAndApologize` 异步方法不包含 `return` 语句，因此此方法返回 <xref:System.Threading.Tasks.Task> 对象。 通过这样可等待 `WaitAndApologize`。 请注意，<xref:System.Threading.Tasks.Task> 类型不包含 `Result` 属性，因为它不具有任何返回值。  

[!code-cs[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns2.cs)]  
  
通过使用 await 语句而不是 await 表达式等待 `WaitAndApologize`，类似于返回 void 的同步方法的调用语句。 Await 运算符的应用程序在这种情况下不生成值。  
  
如同上一个 <xref:System.Threading.Tasks.Task%601> 示例，可以从 await 运算符的应用程序中分离对 `Task_MethodAsync` 的调用，如以下代码所示。 但是，请记住，`Task` 没有 `Result` 属性，并且当 await 运算符应用于 `Task` 时不产生值。  
  
以下代码将调用 `WaitAndApologize` 方法和等待此方法返回的任务分离。  
 
[!code-cs[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns2a.cs#1)]  
 
##  <a name="BKMK_VoidReturnType"></a>Void 返回类型  
在异步事件处理程序中使用 `void` 返回类型，这需要 `void` 返回类型。 对于事件处理程序以外的不返回值的方法，应返回 <xref:System.Threading.Tasks.Task>，因为无法等待返回 `void` 的异步方法。 这种方法的任何调用方必须能够继续完成，而无需等待调用的异步方法完成，并且调用方必须独立于异步方法生成的任何值或异常。  
  
返回 void 的异步方法的调用方无法捕获从该方法引发的异常，且此类未经处理的异常可能会导致应用程序故障。 如果返回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601> 的异步方法中出现异常，此异常将存储于返回的任务中，并在等待该任务时再次引发。 因此，请确保可以产生异常的任何异步方法都具有返回类型 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>，并确保会等待对方法的调用。  
  
有关如何在异步方法中捕捉异常的更多信息，请参阅 [try-catch](../../../../csharp/language-reference/keywords/try-catch.md)。  
  
以下示例定义一个异步事件处理程序。  
 
[!code-cs[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns3.cs)]  
 
## <a name="generalized-async-return-types-and-valuetaskt"></a>通用的异步返回类型和 ValueTask<T>

从 C# 7 开始，异步方法可返回任何具有可访问的 `GetAwaiter` 方法的类型。
 
<xref:System.Threading.Tasks.Task> 和 <xref:System.Threading.Tasks.Task%601> 是引用类型，因此，性能关键路径中的内存分配会对性能产生负面影响，尤其当分配出现在紧凑循环中时。 支持通用返回类型意味着可返回轻量值类型（而不是引用类型），从而避免额外的内存分配。 

.NET 提供 <xref:System.Threading.Tasks.ValueTask%601?displayProperty=fullName> 结构作为返回任务的通用值的轻量实现。 要使用 <xref:System.Threading.Tasks.ValueTask%601?displayProperty=fullName> 类型，必须向项目添加 `System.Threading.Tasks.Extensions` NuGet 包。 如下示例使用 <xref:System.Threading.Tasks.ValueTask%601> 结构检索两个骰子的值。 
  
[!code-cs[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-valuetask.cs)]

## <a name="see-also"></a>另请参阅  
<xref:System.Threading.Tasks.Task.FromResult%2A>   
[演练：使用 Async 和 Await 访问 Web (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
[异步程序中的控制流 (C#)](../../../../csharp/programming-guide/concepts/async/control-flow-in-async-programs.md)   
[Async](../../../../csharp/language-reference/keywords/async.md)   
[await](../../../../csharp/language-reference/keywords/await.md)

