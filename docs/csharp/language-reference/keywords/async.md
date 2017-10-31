---
title: "async（C# 参考）"
ms.date: 2017-05-22
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- async_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- async keyword [C#]
- async method [C#]
- async [C#]
ms.assetid: 16f14f09-b2ce-42c7-a875-e4eca5d50674
caps.latest.revision: 52
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
ms.openlocfilehash: 1dc7ba08d1a79d17d625755a6d60565aee6945e3
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="async-c-reference"></a>async（C# 参考）
使用 `async` 修饰符可将方法、[lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)或[匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)指定为异步。 如果对方法或表达式使用此修饰符，则其称为异步方法。 如下示例定义了一个名为 `ExampleMethodAsync` 的异步方法： 
  
```csharp  
public async Task<int> ExampleMethodAsync()  
{  
    // . . . .  
}  
```  
 
如果不熟悉异步编程，或者不了解异步方法如何在不阻止调用方线程的情况下使用 `await` 关键字完成可能需要长时间运行的工作，请阅读[使用 async 和 await 的异步编程](../../../csharp/programming-guide/concepts/async/index.md)中的介绍。 如下代码见于一种异步方法中，且调用 <xref:System.Net.Http.HttpClient.GetStringAsync%2a?displayProperty=fullName> 方法： 
  
```csharp  
string contents = await httpClient.GetStringAsync(requestUrl);  
```  
  
异步方法同步运行，直至到达其第一个 `await` 表达式，此时会将方法挂起，直到等待的任务完成。 同时，如下节示例中所示，控件将返回到方法的调用方。  
  
如果 `async` 关键字修改的方法不包含 `await` 表达式或语句，则该方法将同步执行。 编译器警告将通知你不包含 `await` 语句的任何异步方法，因为该情况可能表示存在错误。 请参阅[编译器警告（等级 1）CS4014](../../../csharp/language-reference/compiler-messages/cs4014.md)。  
  
 `async` 关键字是上下文关键字，原因在于只有当它修饰方法、lambda 表达式或匿名方法时，它才是关键字。 在所有其他上下文中，都会将其解释为标识符。  
  
## <a name="example"></a>示例  
下面的示例展示了异步事件处理程序 `StartButton_Click` 和异步方法 `ExampleMethodAsync` 之间的控制结构和流程。 此异步方法的结果是 Web 页面的字符数。 此代码适用于在 Visual Studio 中创建的 Windows Presentation Foundation (WPF) 应用或 Windows 应用商店应用；请参见有关设置应用的代码注释。  

可以在 Visual Studio 中将此代码作为 Windows Presentation Foundation (WPF) 应用或 Windows 应用商店应用运行。 需要一个名为 `StartButton` 的按钮控件和一个名为 `ResultsTextBox` 的文本框控件。 切勿忘记设置名称和处理程序，以便获得类似于以下代码的内容：  

```xaml
<Button Content="Button" HorizontalAlignment="Left" Margin="88,77,0,0" VerticalAlignment="Top" Width="75"  
        Click="StartButton_Click" Name="StartButton"/>  
<TextBox HorizontalAlignment="Left" Height="137" Margin="88,140,0,0" TextWrapping="Wrap"   
         Text="&lt;Enter a URL&gt;" VerticalAlignment="Top" Width="310" Name="ResultsTextBox"/>  
```
  
将代码作为 WPF 应用运行：  

- 将此代码粘贴到 MainWindow.xaml.cs 中的 `MainWindow` 类中。  
- 添加对 System.Net.Http 的引用。  
- 为 System.Net.Http 添加一个 `using` 指令。  
  
将此代码作为 Windows 应用商店应用运行：  
- 将此代码粘贴到 MainPage.xaml.cs 中的 `MainPage` 类中。  
- 为 System.Net.Http 和 System.Threading.Tasks 添加 using 指令。  
  
[!code-cs[wpf-async](../../../../samples/snippets/csharp/language-reference/keywords/async/wpf/mainwindow.xaml.cs#1)]
  
> [!IMPORTANT]
>  若要深入了解各项任务以及在等待任务期间所执行的代码，请参阅[使用 async 和 await 的异步编程](../../../csharp/programming-guide/concepts/async/index.md)。 有关使用类似元素的完整 WPF 示例，请参阅[演练：使用 Async 和 Await 访问 Web](../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)。  
  
## <a name="return-types"></a>返回类型  
异步方法可具有以下返回类型：

- <xref:System.Threading.Tasks.Task>
- <xref:System.Threading.Tasks.Task%601>
- [void](../../../csharp/language-reference/keywords/void.md)（应仅用于事件处理程序）。
- 从 C# 7 开始，任何具有可访问的 `GetAwaiter` 方法的类型。 `System.Threading.Tasks.ValueTask<TResult>` 类型属于此类实现。 它通过添加 NuGet 包 `System.Threading.Tasks.Extensions` 的方式可用。 

此异步方法既不能声明任何 [ref](../../../csharp/language-reference/keywords/ref.md) 或 [out](../../../csharp/language-reference/keywords/out.md) 参数，也不能具有<!-- [reference return value](../../programming-guide/classes-and-structs/ref-returns.md) -->引用返回值，但它可以调用具有此类参数的方法。  
  
如果异步方法的 语句指定一个 类型的操作数，则应指定 `Task<TResult>` 作为方法的[返回](../../../csharp/language-reference/keywords/return.md)类型`TResult`。 如果当方法完成时未返回有意义的值，则应使用 `Task`。 即，对方法的调用将返回一个 `Task`，但是当 `Task` 完成时，任何等待 `await` 的所有 `Task` 表达式的计算结果都为 `void`。  
  
你应主要使用 `void` 返回类型来定义事件处理程序，这些处理程序需要此返回类型。 `void` 返回异步方法的调用方不能等待，并且无法捕获该方法引发的异常。  

从 C# 7 开始，返回另一个类型（通常为值类型），该类型具有 `GetAwaiter` 方法，可尽可能减少性能关键代码段中的内存分配。 

有关详细信息和示例，请参阅[异步返回类型](../../../csharp/programming-guide/concepts/async/async-return-types.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>   
 [Await](../../../csharp/language-reference/keywords/await.md)   
 [演练：使用 Async 和 Await 访问 Web](../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [使用 async 和 await 的异步编程](../../../csharp/programming-guide/concepts/async/index.md)

