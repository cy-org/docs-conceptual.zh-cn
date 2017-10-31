---
title: "异常的最佳做法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "异常, 最佳做法"
ms.assetid: f06da765-235b-427a-bfb6-47cd219af539
caps.latest.revision: 28
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 28
---
# 异常的最佳做法
设计良好的应用处理异常和错误以防止应用崩溃。  本文描述处理和创建异常的最佳做法。  
  
## 处理异常  
 以下列表包含一些用于处理应用中的异常的通用准则。  
  
-   正确地使用异常处理代码（`try`\/`catch` 块）。  你也可通过编程方式检查可能发生的条件，而不使用异常处理。  
  
     **编程检查**。  下面的示例使用 `if` 语句检查连接是否关闭。  如果连接未关闭，则此示例将关闭连接而不是引发异常。  
  
     [!code-cpp[Conceptual.Exception.Handling#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#2)]
     [!code-csharp[Conceptual.Exception.Handling#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#2)]
     [!code-vb[Conceptual.Exception.Handling#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#2)]  
  
     **异常处理**。  如果连接未关闭，则以下示例使用 `try`\/`catch` 块检查连接并引发异常。  
  
     [!code-cpp[Conceptual.Exception.Handling#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#3)]
     [!code-csharp[Conceptual.Exception.Handling#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#3)]
     [!code-vb[Conceptual.Exception.Handling#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#3)]  
  
     所选择的方法依赖于预计事件发生的频率。  
  
    -   如果此事件未经常发生（也就是说，如果此事件确实为异常并指示错误（如意外的文件尾）），则使用异常处理。  如果使用异常处理，将在正常条件下执行较少代码。  
  
    -   如果此事件是例行发生的并被视为正常执行的部分，则使用编程方法来检查错误。  当你以编程方式检查错误时，如果发生异常，则会执行更多代码。  
  
-   在可潜在生成异常的代码周围使用 `try`\/`catch` 块，并使用 `finally` 块清理资源（如果需要）。  通过此方法，无论是否发生异常，`try` 语句生成异常，`catch` 语句处理异常，并且 `finally` 语句关闭或释放资源。  
  
-   在 `catch` 块中，始终按从最特定到最不特定的顺序对异常排序。  此方法在将特定异常传递给更常规的 `catch` 块之前处理该异常。  
  
## 创建和引发异常  
 以下列表包含创建自己的异常和引发异常时应遵循的准则。  有关更多详细信息，请参见[异常设计准则](../../../docs/standard/design-guidelines/exceptions.md)。  
  
-   类的设计应使在正常使用中从不引发异常。  例如，<xref:System.IO.FileStream> 类提供可帮助确实是否已到达文件末尾的方法。  这避免了在读取超过文件尾时引发的异常。  下面的示例显示如何读到文件尾。  
  
     [!code-cpp[Conceptual.Exception.Handling#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#5)]
     [!code-csharp[Conceptual.Exception.Handling#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#5)]
     [!code-vb[Conceptual.Exception.Handling#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#5)]  
  
-   引发异常，而不是返回错误代码或 HRESULT。  
  
-   对于极其常见的错误案例，返回 null 而不是引发异常。  极其常见的错误案例可被视为常规控制流。  通过在这些情况下返回 null，可最大程度地减小对应用的性能产生的影响。  
  
-   在大多数情况下，使用预定义的 .NET Framework 异常类型。  仅当预定义的异常类不适用时，引入新异常类。  
  
-   如果根据对象的当前状态，属性集或方法调用不适当，则会引发 <xref:System.InvalidOperationException> 异常。  
  
-   如果传递的参数无效，则会引发 <xref:System.ArgumentException> 异常或派生自 <xref:System.ArgumentException> 的类。  
  
-   对于大多数应用，从 <xref:System.Exception> 类派生自定义异常。  从 <xref:System.ApplicationException> 类派生并没有很大意义。  
  
-   以“Exception”一词作为异常类名的结尾。  例如：  
  
     [!code-cpp[Conceptual.Exception.Handling#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#4)]
     [!code-csharp[Conceptual.Exception.Handling#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#4)]
     [!code-vb[Conceptual.Exception.Handling#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#4)]  
  
-   在 C\# 和 C\+\+ 中，创建自己的异常类别时至少使用三种公共构造函数：默认构造函数、采用字符串消息的构造函数和采用字符串消息和内部异常的构造函数。  有关示例，请参见[如何：创建用户定义的异常](../../../docs/standard/exceptions/how-to-create-user-defined-exceptions.md)。  
  
    1.  <xref:System.Exception.%23ctor>，它使用默认值。  
  
    2.  <xref:System.Exception.%23ctor%28System.String%29>，它接受字符串消息。  
  
    3.  <xref:System.Exception.%23ctor%28System.String%2CSystem.Exception%29>，它接受字符串消息和内部异常。  
  
-   当创建用户定义的异常时，必须确保异常的元数据对远程执行的代码可用，包括当异常跨应用域发生时。  例如，假设应用域 A 创建应用域 B，后者执行引发异常的代码。  应用域 A 若想正确捕获和处理异常，它必须能够找到包含应用域 B 所引发的异常的程序集。  如果包含应用域 B 引发的异常的程序集位于应用域 B 的应用程序基目录下，而不是位于应用域 A 的应用程序基目录下，则应用域 A 将无法找到异常，并且公共语言运行时将引发 <xref:System.IO.FileNotFoundException> 异常。  为避免此情况，可以两种方式部署包含异常信息的程序集：  
  
    -   将程序集放在两个应用域共享的公共应用程序基中。  
  
         \- 或 \-  
  
    -   如果两个应用域不共享一个公共应用程序基，则用强名称为包含异常信息的程序集签名并将其部署到全局程序集缓存中。  
  
-   在每个异常中都包含一个本地化描述字符串。  用户看到的错误消息派生自引发的异常的描述字符串，而不是派生自异常类。  
  
-   通过编程方式使用正确的错误消息（包括结束标点）。  在异常的描述字符串中，每个句子都应以句号结尾。  例如，“记录表已溢出。”将是正确的描述字符串。  
  
-   为编程访问提供 <xref:System.Exception> 属性。  仅当存在附加信息有用的编程方案时，才在异常中提供附加属性（不包括描述字符串）。  例如，<xref:System.IO.FileNotFoundException> 提供 <xref:System.IO.FileNotFoundException.FileName%2A> 属性。  
  
-   堆栈跟踪从引发异常的语句开始，到捕获异常的 `catch` 语句结束。  当决定在何处放置 `throw` 语句时需考虑这一点。  
  
-   使用异常生成器方法。  类从其实现中的不同位置引发同一异常是常见的情况。  为避免过多的代码，应使用帮助器方法创建异常并将其返回。  例如：  
  
     [!code-cpp[Conceptual.Exception.Handling#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#6)]
     [!code-csharp[Conceptual.Exception.Handling#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#6)]
     [!code-vb[Conceptual.Exception.Handling#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#6)]  
  
     或者，使用异常的构造函数生成异常。  这更适合全局异常类，例如 <xref:System.ArgumentException>。  
  
-   引发异常时清理中间结果。  当异常从方法引发时，调用方应能够假定没有副作用。  
  
## 请参阅  
 [异常](../../../docs/standard/exceptions/index.md)