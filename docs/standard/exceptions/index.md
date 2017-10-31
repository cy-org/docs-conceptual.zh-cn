---
title: "处理和引发异常"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exceptions [.NET Framework], handling
- runtime, exceptions
- filtering exceptions
- errors [.NET Framework], exceptions
- exceptions [.NET Framework], throwing
- exceptions [.NET Framework]
- common language runtime, exceptions
ms.assetid: f99a1d29-a2a8-47af-9707-9909f9010735
caps.latest.revision: 16
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 5d44996042d167c029291f2b454dc1a22cfbcfb4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="handling-and-throwing-exceptions-in-net"></a>在 .NET 中处理和引发异常

应用程序必须能够以一致的方式处理执行期间发生的错误。 .NET 提供一种以统一方式向应用程序报错的模型：.NET 操作通过引发异常来指示故障。

## <a name="exceptions"></a>异常

异常是执行程序遇到的所有错误条件或意外行为。 异常可能由你的代码或调用的代码（如共享库）中的错误、不可用的操作系统资源、运行时遇到的意外情况（如无法验证的代码）等引发。 应用程序可从这些情况中的一些中恢复，但无法从其他情况中恢复。 尽管可以从大多数应用程序异常中恢复，但不能从大多数运行时异常中恢复。

在 .NET 中，异常是从 [System.Exception](xref:System.Exception) 类继承的对象。 异常引发自发生问题的代码区域。 异常在堆栈中向上传递，直到应用程序对其进行处理或者程序终止。

## <a name="exceptions-vs-traditional-error-handling-methods"></a>异常与传统的错误处理方法

传统上，语言的错误处理模型依赖语言检测错误和针对错误查找其处理程序的独特方式，或者依赖操作系统提供的错误处理机制。 .NET 实现异常处理的方式有以下优点：

- 引发和处理异常的方式与 .NET 编程语言的相同。

- 处理异常不需要任何特定的语言语法，但允许每种语言定义自己的语法。

- 可跨进程，甚至跨计算机边界引发异常。

- 可向应用程序添加异常处理代码以提高程序的可靠性。

异常相较于其他错误通知方法（如返回代码）具有多种优势。 故障不会被忽略掉，因为如果引发了异常且未得到解决，运行时会终止应用程序。 因为代码未能检查出是否存在故障返回代码，所以无效值不会继续在系统中传播。 

## <a name="common-exceptions"></a>常见异常

下表列出了一些常见的异常，以及会引发这些异常的原因的示例。

| 异常类型 | 基类型 | 描述 | 示例 |
| -------------- | --------- | ----------- | ------- |
| @System.Exception | @System.Object | 所有异常的基类。 | 无（使用此异常的派生类）。 |
| @System.IndexOutOfRangeException | @System.Exception | 仅当错误地对数组进行索引时，才由运行时引发。 | 在数组的有效范围外对数组进行索引：`arr[arr.Length+1]` |
| @System.NullReferenceException | @System.Exception | 仅当引用 null 对象时，才由运行时引发。 | `object o = null; o.ToString();` |
| @System.InvalidOperationException | @System.Exception | 当处于无效状态时，由方法引发。 | 从基础集合删除项后调用 `Enumerator.GetNext()`。 |
| @System.ArgumentException | @System.Exception | 所有自变量异常的基类。 | 无（使用此异常的派生类）。 |
| @System.ArgumentNullException | @System.Exception | 由不允许参数为 null 的方法引发。 | `String s = null; "Calculate".IndexOf (s);` |
| @System.ArgumentOutOfRangeException | @System.Exception | 由验证自变量是否位于给定范围内的方法引发。 | `String s = "string"; s.Substring(s.Length+1);` |

## <a name="see-also"></a>另请参阅

* [异常类和属性](exception-class-and-properties.md)
* [如何：使用 Try-Catch 块捕捉异常](how-to-use-the-try-catch-block-to-catch-exceptions.md)
* [如何：在 Catch 块中使用特定异常](how-to-use-specific-exceptions-in-a-catch-block.md)
* [如何：显式引发异常](how-to-explicitly-throw-exceptions.md)
* [如何：创建用户定义的异常](how-to-create-user-defined-exceptions.md)
* [使用用户筛选的异常处理程序](using-user-filtered-exception-handlers.md)
* [如何：使用 Finally 块](how-to-use-finally-blocks.md)
* [处理 COM 互操作异常](handling-com-interop-exceptions.md)
* [与异常有关的最佳做法](best-practices-for-exceptions.md)

若要了解有关 .NET 中异常的工作方式的详细信息，请参阅[运行时中每个开发人员都需要了解的有关异常的事项](https://github.com/dotnet/coreclr/blob/master/Documentation/botr/exceptions.md)。

