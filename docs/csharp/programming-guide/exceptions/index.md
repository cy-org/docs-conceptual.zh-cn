---
title: "异常和异常处理（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exception handling [C#]
- exceptions [C#]
- C# language, exceptions
ms.assetid: 0001887f-4fa2-47e2-8034-2819477e2344
caps.latest.revision: 33
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
ms.openlocfilehash: e372cfa3239c39af86a29cda06b5817f0aeff0a2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="exceptions-and-exception-handling-c-programming-guide"></a>异常和异常处理（C# 编程指南）
C# 语言的异常处理功能有助于处理在程序运行期间发生的任何意外或异常情况。 异常处理功能使用 `try`、`catch` 和 `finally` 关键字来尝试执行可能失败的操作、在你确定合理的情况下处理故障，以及在事后清除资源。 公共语言运行时 (CLR)、.NET Framework/任何第三方库或应用程序代码都可以生成异常。 异常是使用 `throw` 关键字创建而成。  
  
 在许多情况下，异常并不是由代码直接调用的方法抛出，而是由调用堆栈中再往下的另一方法抛出。 如果出现这种情况，CLR 会展开堆栈，同时针对特定异常类型查找包含 `catch` 代码块的方法，并执行找到的首个此类 `catch` 代码块。 如果在调用堆栈中找不到相应的 `catch` 代码块，将会终止进程并向用户显示消息。  
  
 在以下示例中，方法用于测试除数是否为零，并捕获相应的错误。 如果没有异常处理功能，此程序将终止，并显示 **DivideByZeroException was unhandled** 错误。  
  
 [!code-cs[csProgGuideExceptions#18](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exceptions-and-exception-handling_1.cs)]  
  
## <a name="exceptions-overview"></a>异常概述  
 异常具有以下属性：  
  
-   异常是最终全都派生自 `System.Exception` 的类型。  
  
-   在可能抛出异常的语句周围使用 `try` 代码块。  
  
-   在 `try` 代码块中出现异常后，控制流会跳转到调用堆栈中任意位置上的首个相关异常处理程序。 在 C# 中，`catch` 关键字用于定义异常处理程序。  
  
-   如果给定的异常没有对应的异常处理程序，那么程序会停止执行，并显示错误消息。  
  
-   除非可以处理异常并让应用程序一直处于已知状态，否则不捕获异常。 如果捕获 `System.Exception`，使用 `catch` 代码块末尾的 `throw` 关键字重新抛出异常。  
  
-   如果 `catch` 代码块定义异常变量，可以用它来详细了解所发生的异常类型。  
  
-   使用 `throw` 关键字，程序可以显式生成异常。  
  
-   异常对象包含错误详细信息，如调用堆栈的状态和错误的文本说明。  
  
-   即使有异常抛出，`finally` 代码块中的代码仍会执行。 使用 `finally` 代码块可释放资源。例如，关闭在 `try` 代码块中打开的任何流或文件。  
  
-   .NET Framework 中的托管异常在 Win32 结构化异常处理机制的基础之上实现。 有关详细信息，请参阅[结构化异常处理 (C/C++)](/cpp/cpp/structured-exception-handling-c-cpp) 和[速成教程：深入了解 Win32 结构化异常处理](http://go.microsoft.com/fwlink/?LinkId=119654)。  
  
## <a name="related-sections"></a>相关章节  
 若要详细了解异常和异常处理，请参阅以下主题：  
  
-   [使用异常](../../../csharp/programming-guide/exceptions/using-exceptions.md)  
  
-   [异常处理](../../../csharp/programming-guide/exceptions/exception-handling.md)  
  
-   [创建和引发异常](../../../csharp/programming-guide/exceptions/creating-and-throwing-exceptions.md)  
  
-   [编译器生成的异常](../../../csharp/programming-guide/exceptions/compiler-generated-exceptions.md)  
  
-   [如何：使用 try/catch 处理异常（C# 编程指南）](../../../csharp/programming-guide/exceptions/how-to-handle-an-exception-using-try-catch.md)  
  
-   [如何：使用 finally 执行清理代码](../../../csharp/programming-guide/exceptions/how-to-execute-cleanup-code-using-finally.md)  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.SystemException>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C 关键字](../../../csharp/language-reference/keywords/index.md)   
 [throw](../../../csharp/language-reference/keywords/throw.md)   
 [try-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)   
 [异常](../../../standard/exceptions/index.md)   
 [异常层次结构](http://msdn.microsoft.com/library/f7d68675-be06-40fb-a555-05f0c5a6f66b)   
 [编写可靠的 .NET 代码](http://go.microsoft.com/fwlink/?LinkId=112400)   
 [用于特定异常的小型转储](http://go.microsoft.com/fwlink/?LinkId=112408)

