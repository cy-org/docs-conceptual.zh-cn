---
title: "How to: Handle Exceptions in a PLINQ Query | Microsoft Docs"
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
  - "PLINQ queries, how to handle exceptions"
ms.assetid: 8d56ff9b-a571-4d31-b41f-80c0b51b70a5
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# How to: Handle Exceptions in a PLINQ Query
本主题中的第一个示例演示如何处理在 PLINQ 查询执行时可能从中引发的 <xref:System.AggregateException?displayProperty=fullName>。  第二个示例演示如何将 try\-catch 块放在委托内，尽可能靠近将会引发异常的位置。  通过这种方式，一旦发生异常，您就可以捕获它们并且可能继续执行查询。  如果允许异常向上冒泡回到联接线程，则查询操作也许可以在引发异常后继续处理一些项目。  
  
 在某些情况下，当 PLINQ 回退到顺序执行并发生异常时，可能会直接传播该异常，而不是包装到 <xref:System.AggregateException> 中。  此外，始终可以直接传播 <xref:System.Threading.ThreadAbortException>。  
  
> [!NOTE]
>  当启用“仅我的代码”时，Visual Studio 将在引发异常的行上中断运行，并显示错误消息“异常未由用户代码处理”。此错误是良性的。  可以按 F5 从中断处继续运行，并查看在以下示例中演示的异常处理行为。  若要阻止 Visual Studio 在出现第一个错误时中断运行，只需在**“工具”\-\>“选项”\-\>“调试”\-\>“常规”**下取消选中“仅我的代码”复选框即可。  
>   
>  本示例旨在演示用法，运行速度可能不如等效的顺序 LINQ to Objects 查询快。  有关加速的更多信息，请参见[Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)。  
  
## 示例  
 此示例演示如何将 try\-catch 块放在执行查询以捕获任何引发的 <xref:System.AggregateException?displayProperty=fullName> 的代码的周围。  
  
 [!code-csharp[PLINQ#41](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#41)]
 [!code-vb[PLINQ#41](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#41)]  
  
 在此示例中，查询在引发异常后无法继续。  到应用程序代码捕获异常时，PLINQ 已经在所有线程上停止了查询。  
  
## 示例  
 下面的示例演示如何将 try\-catch 块放在委托中，以便能够捕获异常并继续执行查询。  
  
 [!code-csharp[PLINQ#42](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#42)]
 [!code-vb[PLINQ#42](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#42)]  
  
## 编译代码  
  
-   若要编译并运行这些示例，请将它们复制到“PLINQ 数据示例”示例中，并从 Main 中调用方法。  
  
## 可靠编程  
 除非您知道如何处理异常因而不会损坏程序的状态，否则请不要捕获异常。  
  
## 请参阅  
 <xref:System.Linq.ParallelEnumerable>   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)