---
title: "如何：使用 Finally 块 | Microsoft Docs"
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
  - "ArgumentOutOfRangeException 类"
  - "异常, finally 块"
  - "异常, try/catch 块"
  - "finally 块"
  - "try/catch 块"
ms.assetid: 4b9c0137-04af-4468-91d1-b9014df8ddd2
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使用 Finally 块
异常发生时，执行将终止，并且控制交给最近的异常处理程序。  这通常意味着不执行希望总是调用的代码行。  有些资源清理（如关闭文件）必须总是执行，即使有异常发生。  为实现这一点，可以使用 Finally 块。  Finally 块总是执行，不论是否有异常发生。  
  
 下面的代码示例使用 try\/catch 块捕获 <xref:System.ArgumentOutOfRangeException>。  `Main` 方法创建两个数组并尝试将一个数组复制到另一个数组。  该操作生成 **ArgumentOutOfRangeException**，同时错误被写入控制台。  Finally 块执行，不论复制操作的结果如何。  
  
## 示例  
 [!code-cpp[CodeTryCatchFinallyExample#3](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeTryCatchFinallyExample/CPP/source2.cpp#3)]
 [!code-csharp[CodeTryCatchFinallyExample#3](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeTryCatchFinallyExample/CS/source2.cs#3)]
 [!code-vb[CodeTryCatchFinallyExample#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeTryCatchFinallyExample/VB/source2.vb#3)]  
  
## 请参阅  
 [如何：使用 Try\/Catch 块捕捉异常](../../../docs/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions.md)   
 [如何：显式引发异常](../../../docs/standard/exceptions/how-to-explicitly-throw-exceptions.md)   
 [如何：创建用户定义的异常](../../../docs/standard/exceptions/how-to-create-user-defined-exceptions.md)   
 [异常处理基础知识](../../../docs/standard/exceptions/exception-handling-fundamentals.md)