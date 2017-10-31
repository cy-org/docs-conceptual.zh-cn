---
title: "try-catch（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- try
- try_CSharpKeyword
- catch
- catch_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- catch keyword [C#]
- try-catch statement [C#]
ms.assetid: cb5503c7-bfa1-4610-8fc2-ddcd2e84c438
caps.latest.revision: 45
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 81117b1419c2a9c3babd6a7429052e2b23e08a70
ms.openlocfilehash: 47e4c298c20e7adde0e427f0a547904db2f96d37
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="try-catch-c-reference"></a>try-catch（C# 参考）
Try-catch 语句包含一个后接一个或多个 `catch` 子句的 `try` 块，这些子句指定不同异常的处理程序。  
  
## <a name="remarks"></a>备注  
 引发异常时，公共语言运行时 (CLR) 查找处理此异常的 `catch` 语句。 如果当前正在执行的方法不包含此类 `catch` 块，则 CLR 查看调用了当前方法的方法，并以此类推遍历调用堆栈。 如果未找到任何 `catch` 块，则 CLR 向用户显示一条未处理的异常消息，并停止执行程序。  
  
 `try` 块包含可能导致异常的受保护的代码。 将执行此块，直至引发异常或其成功完成。 例如，强制转换 `null` 对象的以下尝试会引发 <xref:System.NullReferenceException> 异常：  
  
```csharp  
object o2 = null;  
try  
{  
    int i2 = (int)o2;   // Error  
}  
```  
  
 尽管可以不带参数使用 `catch` 子句来捕获任何类型的异常，但不推荐这种用法。 一般情况下，只应捕获你知道如何从其恢复的异常。 因此，应始终指定派生自 <xref:System.Exception?displayProperty=nameWithType> 的对象参数，例如：  
  
```csharp  
catch (InvalidCastException e)   
{  
}  
```  
  
 可以使用同一 try-catch 语句中的多个特定 `catch` 子句。 在这种情况下，`catch` 子句的顺序很重要，因为 `catch` 子句是按顺序检查的。 在使用更笼统的子句之前获取特定性更强的异常。 如果捕获块的排序使得永不会达到之后的块，则编译器将产生错误。  
  
 筛选想要处理的异常的一种方式是使用 `catch` 参数。  也可以使用谓词表达式进一步检查该异常以决定是否要对其进行处理。  如果谓词表达式返回 false，则继续搜索处理程序。  
  
```csharp  
catch (ArgumentException e) when (e.ParamName == "…")  
{  
}  
```  
  
 异常筛选器要优于捕获和重新引发（如下所述），因为筛选器将保留堆栈不受损坏。  如果之后的处理程序转储堆栈，可以查看到异常的原始来源，而不只是重新引发它的最后一个位置。  异常筛选器表达式的一个常见用途是日志记录。  可以创建一个始终返回 false 并输出到日志的谓词函数，而且可以在异常通过时进行记录，无需处理并重新引发它们。  
  
 可在 `catch` 块中使用 [throw](../../../csharp/language-reference/keywords/throw.md) 语句以重新引发已由 `catch` 语句捕获的异常。 下面的示例从 <xref:System.IO.IOException> 异常提取源信息，然后向父方法引发异常。  
  
```csharp  
catch (FileNotFoundException e)  
{  
    // FileNotFoundExceptions are handled here.  
}  
catch (IOException e)  
{  
    // Extract some information from this exception, and then   
    // throw it to the parent method.  
    if (e.Source != null)  
        Console.WriteLine("IOException source: {0}", e.Source);  
    throw;  
}  
```  
  
 你可以捕获一个异常而引发一个不同的异常。 执行此操作时，请指定作为内部异常捕获的异常，如以下示例所示。  
  
```csharp  
catch (InvalidCastException e)   
{  
    // Perform some action here, and then throw a new exception.  
    throw new YourCustomException("Put your error message here.", e);  
}  
```  
  
 当指定的条件为 true 时，你还可以重新引发异常，如以下示例所示。  
  
```csharp  
catch (InvalidCastException e)  
{  
    if (e.Data == null)  
    {  
        throw;  
    }  
    else  
    {  
        // Take some action.  
    }  
 }  
```  
  
 从 `try` 块内，仅初始化在其中声明的变量。 否则，在完成执行块之前，可能会出现异常。 例如，在下面的代码示例中，变量 `n` 在 `try` 块内部初始化。 尝试在 `Write(n)` 语句的 `try` 块外部使用此变量将生成编译器错误。  
  
```csharp  
static void Main()   
{  
    int n;  
    try   
    {  
        // Do not initialize this variable here.  
        n = 123;  
    }  
    catch  
    {  
    }  
    // Error: Use of unassigned local variable 'n'.  
    Console.Write(n);  
}  
```  
  
 有关 catch 的详细信息，请参阅 [try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)。  
  
## <a name="exceptions-in-async-methods"></a>异步方法中的异常  
 异步方法由 [async](../../../csharp/language-reference/keywords/async.md) 修饰符标记，通常包含一个或多个 await 表达式或语句。 await 表达式将 [await](../../../csharp/language-reference/keywords/await.md) 运算符应用于 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>。  
  
 当控件到达异步方法中的 `await` 时，将挂起方法中的进度，直到所等待的任务完成。 任务完成后，可以在方法中恢复执行。 有关详细信息，请参阅[使用 async 和 await 的异步编程](../../../csharp/programming-guide/concepts/async/index.md)和[异步程序中的控制流](../../../csharp/programming-guide/concepts/async/control-flow-in-async-programs.md)。  
  
 应用了 `await` 的完成任务可能由于返回此任务的方法中存在未处理的异常而处于错误状态。 等待该任务引发异常。 如果取消了返回任务的异步进程，此任务最后也可能为已取消状态。 等待已取消的任务引发 `OperationCanceledException`。 有关如何取消异步进程的详细信息，请参阅[微调异步应用程序](http://msdn.microsoft.com/library/daaa32ea-c84c-4761-8230-c8292ffebd74)。  
  
 若要捕获异常，请在 `try` 块中等待任务并在关联的 `catch` 块中捕获异常。 相关示例，请参见“示例”一节。  
  
 任务可能处于错误状态，因为等待的异步方法中发生了多个异常。 例如，任务可能是对 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 调用的结果。 当等待此类任务时，仅捕捉到其中一个异常，而且你无法预测将会捕获到哪个异常。 相关示例，请参见“示例”一节。  
  
## <a name="example"></a>示例  
 在下面的示例中，`try` 块包含对可能引发异常的 `ProcessString` 方法的调用。 `catch` 子句包含只在屏幕上显示一条消息的异常处理程序。 当从 `MyMethod` 内部调用 `throw` 语句时，系统将查找 `catch` 语句并显示消息 `Exception caught`。  
  
 [!code-cs[csrefKeywordsExceptions#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_1.cs)]  
  
## <a name="example"></a>示例  
 在下面的示例中，使用了两个 catch 块，并捕获到最先出现的最具体的异常。  
  
 若要捕获最不具体的异常，你可以将 `ProcessString` 中的 throw 语句替换为以下语句：`throw new Exception()`。  
  
 如果将最不具体的 catch 块置于示例中第一个，将显示以下错误消息：`A previous catch clause already catches all exceptions of this or a super type ('System.Exception')`。  
  
 [!code-cs[csrefKeywordsExceptions#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_2.cs)]  
  
## <a name="example"></a>示例  
 下面的示例阐释异步方法的异常处理。 若要捕获异步任务引发的异常，将 `await` 表达式置于 `try` 块中，并在 `catch` 块中捕获该异常。  
  
 在示例中取消注释 `throw new Exception` 行以演示异常处理。 任务的 `IsFaulted` 属性设置为 `True`，任务的 `Exception.InnerException` 属性设置为异常，并在 `catch` 块中捕获该异常。  
  
 取消注释 `throw new OperationCancelledException` 行以演示在取消异步进程时发生的情况。 任务的 `IsCanceled` 属性设置为 `true`，并在 `catch` 块中捕获异常。 在某些不适用于此示例的情况下，任务的 `IsFaulted` 属性设置为 `true` 且 `IsCanceled` 设置为 `false`。  
  
 [!code-cs[csAsyncExceptions#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_3.cs)]  
  
## <a name="example"></a>示例  
 下面的示例阐释了在多个任务可能导致多个异常的情况中的异常处理。 `try` 块等待由 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 的调用返回的任务。 应用了 WhenAll 的三个任务完成后，该任务完成。  
  
 三个任务中的每一个都会导致异常。 `catch` 块循环访问异常，这些异常位于由 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 返回的任务的 `Exception.InnerExceptions` 属性中。  
  
 [!code-cs[csAsyncExceptions#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_4.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [try、throw 和 catch 语句 (C++)](/cpp/cpp/try-throw-and-catch-statements-cpp)   
 [异常处理语句](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [throw](../../../csharp/language-reference/keywords/throw.md)   
 [try-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [如何：显式引发异常](https://msdn.microsoft.com/library/xhcbs8fz)

