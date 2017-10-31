---
title: "Using Objects That Implement IDisposable | Microsoft Docs"
ms.custom: ""
ms.date: "04/07/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Dispose method"
  - "try/finally block"
  - "garbage collection, encapsulating resources"
ms.assetid: 81b2cdb5-c91a-4a31-9c83-eadc52da5cf0
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Using Objects That Implement IDisposable
公共语言运行时的垃圾回收器将回收非托管对象使用的内存，而使用非托管资源的类型将实现 <xref:System.IDisposable> 接口以允许回收此非托管内存。  在使用完实现 <xref:System.IDisposable> 的对象后，应调用该对象的 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 实现。  可以通过两种方法执行此操作：  
  
-   通过使用 C\# **Using** 语句或 Visual Basic `Using` 语句。  
  
-   通过实现 `try`\/`finally` 块。  
  
## using 语句  
 C\# 中的 **using** 语句和 Visual Basic 中的 `Using` 语句可简化你创建和清理对象而必须编写的代码。  **using** 语句获得一个或多个资源，执行你指定的语句，并自动处置对象。  但是，**using** 语句仅对在用于构造对象的方法的范围内使用的对象有用。  
  
 以下示例使用 `using` 语句创建并发布 <xref:System.IO.StreamReader?displayProperty=fullName> 对象。  
  
 [!code-csharp[Conceptual.Disposable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using1.cs#1)]
 [!code-vb[Conceptual.Disposable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using1.vb#1)]  
  
 请注意，虽然 <xref:System.IO.StreamReader> 类实现 <xref:System.IDisposable> 接口（这指示使用非托管资源），但此示例不显式调用 <xref:System.IO.StreamReader.Dispose%2A?displayProperty=fullName> 方法。  当 C\# 或 Visual Basic 编译器遇到 `using` 语句时，它会发出与以下显式包含 `try`\/`finally` 块的代码等效的中间语言 \(IL\)。  
  
 [!code-csharp[Conceptual.Disposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using3.cs#3)]
 [!code-vb[Conceptual.Disposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using3.vb#3)]  
  
 使用 C\# 的 **using** 语句，也可以在单个语句（该语句在内部等效于嵌套的 **using** 语句）中获取多个资源。  下面的示例实例化两个 <xref:System.IO.StreamReader> 对象以读取两个不同文件的内容。  
  
 [!code-csharp[Conceptual.Disposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using4.cs#4)]  
  
## Try\/finally 块  
 你可以选择直接实现 `try`\/`finally` 块，而不是将 `try`\/`finally` 块包装在 `using` 语句中。  这可以是私有编码样式，或者你可能出于下列原因之一需要这样做：  
  
-   包含 `catch` 块可处理 `try` 块中引发的任何异常。  否则，不会处理 `using` 语句引发的任何异常，`using` 块中引发的任何异常也是如此，前提是 `try`\/`catch` 块不存在。  
  
-   实例化实现 <xref:System.IDisposable>（其范围对于声明它的块是非本地的）的对象。  
  
 下面的示例与上一个示例类似，只不过该示例使用 `try`\/`catch`\/`finally` 块实例化、使用和处理 <xref:System.IO.StreamReader> 对象，同时处理由 <xref:System.IO.StreamReader> 构造函数和其 <xref:System.IO.StreamReader.ReadToEnd%2A> 方法引发的任何异常。  请注意，`finally` 块中的代码检查实现 <xref:System.IDisposable> 的对象在其调用 <xref:System.IDisposable.Dispose%2A> 方法之前不为 `null`。  此操作失败会导致运行时发生 <xref:System.NullReferenceException> 异常。  
  
 [!code-csharp[Conceptual.Disposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using5.cs#6)]
 [!code-vb[Conceptual.Disposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using5.vb#6)]  
  
 如果你选择实现或必须实现 `try`\/`finally` 块，则可遵循此基本模式，因为你的编程语言不支持 `using` 语句但允许直接调用 <xref:System.IDisposable.Dispose%2A> 方法。  
  
 如果你的语言不支持直接调用 <xref:System.IDisposable.Dispose%2A> 方法（例如，在 C\+\+ 中），你通常可使用你语言的析构函数语法。  
  
## 请参阅  
 [Cleaning Up Unmanaged Resources](../../../docs/standard/garbage-collection/unmanaged.md)   
 [using 语句](../Topic/using%20Statement%20\(C%23%20Reference\).md)   
 [Using 语句](../Topic/Using%20Statement%20\(Visual%20Basic\).md)