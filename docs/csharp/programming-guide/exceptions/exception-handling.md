---
title: "异常处理（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exception handling [C#], about exception handling
- exceptions [C#], handling
ms.assetid: b4e4ecf2-b907-4e58-891f-2563762258e9
caps.latest.revision: 24
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
ms.openlocfilehash: ab03e00a6b62d0c737c90fdb489be2a78f7ab6af
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="exception-handling-c-programming-guide"></a>异常处理（C# 编程指南）
C# 程序员使用 [try](../../../csharp/language-reference/keywords/try-catch.md) 块来对可能受异常影响的代码进行分区。 关联的 [catch](../../../csharp/language-reference/keywords/try-catch.md) 块用于处理生成的任何异常。 [finally](../../../csharp/language-reference/keywords/try-finally.md) 块包含无论 `try` 块中是否引发异常都会运行的代码，如发布 `try` 块中分配的资源。 `try` 块需要一个或多个关联的 `catch` 块或一个 `finally` 块，或两者皆之。  
  
 下面的示例演示 `try-catch` 语句、`try-finally` 语句和 `try-catch-finally` 语句。  
  
 [!code-cs[csProgGuideExceptions#6](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_1.cs)]  
  
 [!code-cs[csProgGuideExceptions#7](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_2.cs)]  
  
 [!code-cs[csProgGuideExceptions#8](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_3.cs)]  
  
 一个不具有 `catch` 或 `finally` 块的 `try` 块会导致编译器错误。  
  
## <a name="catch-blocks"></a>catch 块  
 `catch` 块可以指定要捕获的异常的类型。 该类型规范称为异常筛选器。 异常类型应派生自 <xref:System.Exception>。 一般情况下，不要将 <xref:System.Exception> 指定为异常筛选器，除非了解如何处理可能在 `try` 块中引发的所有异常，或者已在 `catch` 块的末尾处包括了 [throw](../../../csharp/language-reference/keywords/throw.md) 语句。  
  
 可将具有不同异常筛选器的多个 `catch` 块链接在一起。 代码中 `catch` 块的计算顺序为从上到下，但针对引发的每个异常，仅执行一个 `catch` 块。 将执行指定所引发的异常的确切类型或基类的第一个 `catch` 块。 如果没有 `catch` 块指定匹配的异常筛选器，则将选择不具有筛选器的 `catch` 块（如果语句中存在）。 务必首先定位具有最具体的（即，最底层派生的）异常类型的 `catch` 块。  
  
 应当会在下列条件为 true 时捕获到异常：  
  
-   能够很好地理解可能会引发异常的原因，并且可以实现特定的恢复，例如捕获 <xref:System.IO.FileNotFoundException> 对象时提示用户输入新文件名。  
  
-   可以创建和引发一个新的、更具体的异常。  
  
     [!code-cs[csProgGuideExceptions#9](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_4.cs)]  
  
-   想要先对异常进行部分处理，然后再将其传递以进行额外处理。 在下面的示例中，`catch` 块用于在重新引发异常之前将条目添加到错误日志。  
  
     [!code-cs[csProgGuideExceptions#10](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_5.cs)]  
  
## <a name="finally-blocks"></a>Finally 块  
 `finally` 块让你可以清理在 `try` 块中所执行的操作。 如果存在 `finally` 块，将在执行 `try` 块和任何匹配的 `catch` 块之后，最后执行它。 无论是否会引发异常或找到匹配异常类型的 `catch` 块，`finally` 块都将始终运行。  
  
 `finally` 块可用于发布资源（如文件流、数据库连接和图形句柄）而无需等待运行时中的垃圾回收器来完成对象。 有关详细信息，请参阅 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)。  
  
 在下面的示例中，`finally` 块用于关闭在 `try` 块中打开的文件。 请注意，在关闭文件之前，将检查文件句柄的状态。 如果 `try` 块不能打开文件，则文件句柄仍将具有值 `null` 且 `finally` 块不会尝试将其关闭。 或者，如果在 `try` 块中成功打开文件，则 `finally` 块将关闭打开的文件。  
  
 [!code-cs[csProgGuideExceptions#11](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_6.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [异常和异常处理](../../../csharp/programming-guide/exceptions/index.md)   
 [try-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)   
 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)

