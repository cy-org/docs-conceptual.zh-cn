---
title: "如何：在 Catch 块中使用特定异常 | Microsoft Docs"
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
  - "捕捉块"
  - "异常, try/catch 块"
  - "try/catch 块"
ms.assetid: 12af9ff3-8587-4f31-90cf-6c2244e0fdae
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：在 Catch 块中使用特定异常
发生异常时，异常沿堆栈向上传递，每个 Catch 块都有机会处理它。  Catch 语句的顺序很重要。  将针对特定异常的 Catch 块放在常规异常 Catch 块的前面，否则编译器可能会发出错误。  确定正确 Catch 块的方法是将异常的类型与 Catch 块中指定的异常名称进行匹配。  如果没有特定的 Catch 块，则由可能存在的常规 Catch 块捕捉异常。  
  
 下面的代码示例使用 try\/catch 块捕获 <xref:System.InvalidCastException>。  该示例创建一个名为 `Employee` 的类，它带有一个属性：职员级别 \(`Emlevel`\)。  `PromoteEmployee` 方法取得对象并增加职员级别。  将 <xref:System.DateTime> 实例传递给 `PromoteEmployee` 方法时，发生 **InvalidCastException**。  
  
## 示例  
 [!code-cpp[CatchException#2](../../../samples/snippets/cpp/VS_Snippets_CLR/CatchException/CPP/catchexception1.cpp#2)]
 [!code-csharp[CatchException#2](../../../samples/snippets/csharp/VS_Snippets_CLR/CatchException/CS/catchexception1.cs#2)]
 [!code-vb[CatchException#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CatchException/VB/catchexception1.vb#2)]  
  
 公共语言运行时捕捉 Catch 块没有捕捉的异常。  根据运行时的配置，或者出现一个调试对话框，或者程序停止执行并出现一个包含异常信息的对话框。  有关调试的信息，请参见[调试和分析应用程序](../../../docs/framework/debug-trace-profile/index.md)。  
  
## 请参阅  
 [如何：使用 Try\/Catch 块捕捉异常](../../../docs/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions.md)   
 [如何：显式引发异常](../../../docs/standard/exceptions/how-to-explicitly-throw-exceptions.md)   
 [如何：创建用户定义的异常](../../../docs/standard/exceptions/how-to-create-user-defined-exceptions.md)   
 [如何：使用 Finally 块](../../../docs/standard/exceptions/how-to-use-finally-blocks.md)   
 [异常类和属性](../../../docs/standard/exceptions/exception-class-and-properties.md)   
 [异常处理基础知识](../../../docs/standard/exceptions/exception-handling-fundamentals.md)