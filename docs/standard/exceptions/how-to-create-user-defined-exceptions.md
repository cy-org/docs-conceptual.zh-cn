---
title: "如何：创建用户定义的异常 | Microsoft Docs"
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
  - "异常, 示例"
  - "异常, 用户定义的"
  - "用户定义的异常"
ms.assetid: 25819a5a-f915-4fc8-b924-a76915674e04
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：创建用户定义的异常
如果希望用户能以编程方式区分一些错误条件，您可以创建自己的用户定义的异常。  .NET Framework 提供根本上从基类 <xref:System.Exception> 派生的异常类的层次结构。  这些类中的每一个都定义一个特定的异常，因此在很多情况下只需捕捉该异常。  您也可以通过从 <xref:System.Exception> 类派生来创建自己的异常类。  
  
 创建自己的异常时，好的编码做法是以“Exception”这个词作为用户定义的异常类名的结尾。如下面的示例所示实现三个推荐的公共构造函数也是好的做法。  
  
> [!NOTE]
>  当使用远程处理时，对于任何用户定义的异常的元数据，都必须确保其在服务器（被调用方）和客户端（代理对象或调用方）上均可用。  例如，在单独的应用程序域中调用方法的代码必须能够找到包含远程调用引发的异常的程序集。  有关更多信息，请参见[处理异常的最佳做法](../../../docs/standard/exceptions/best-practices-for-exceptions.md)。  
  
 在下面的示例中，从 <xref:System.Exception> 派生了一个新异常类 `EmployeeListNotFoundException`。  该类中定义了三个构造函数，每个构造函数使用不同的参数。  
  
## 示例  
 [!code-cpp[dg_exceptionDesign#14](../../../samples/snippets/cpp/VS_Snippets_CLR/dg_exceptionDesign/cpp/example2.cpp#14)]
 [!code-csharp[dg_exceptionDesign#14](../../../samples/snippets/csharp/VS_Snippets_CLR/dg_exceptionDesign/cs/example2.cs#14)]
 [!code-vb[dg_exceptionDesign#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/dg_exceptionDesign/vb/example2.vb#14)]  
  
## 请参阅  
 [如何：使用 Try\/Catch 块捕捉异常](../../../docs/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions.md)   
 [如何：在 Catch 块中使用特定异常](../../../docs/standard/exceptions/how-to-use-specific-exceptions-in-a-catch-block.md)   
 [异常的最佳做法](../../../docs/standard/exceptions/best-practices-for-exceptions.md)   
 [异常处理基础知识](../../../docs/standard/exceptions/exception-handling-fundamentals.md)