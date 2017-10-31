---
title: "How to: Cancel a Parallel.For or ForEach Loop | Microsoft Docs"
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
  - "parallel foreach loop, how to cancel"
  - "parallel for loops, how to cancel"
ms.assetid: 9d19b591-ea95-4418-8ea7-b6266af9905b
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# How to: Cancel a Parallel.For or ForEach Loop
<xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> 和 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 方法支持通过使用取消标记进行取消。  有关常规取消的更多信息，请参见[取消](../../../docs/standard/threading/cancellation-in-managed-threads.md)。  在并行循环中，您在 <xref:System.Threading.Tasks.ParallelOptions> 参数中向方法提供 <xref:System.Threading.CancellationToken>，然后将并行调用置于 try\-catch 块中。  
  
## 示例  
 下面的示例演示如何取消对 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 的调用。  您可以将同样的方法应用于 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> 调用。  
  
 [!code-csharp[TPL_Parallel#29](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallel_cancel.cs#29)]
 [!code-vb[TPL_Parallel#29](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/cancelloop.vb#29)]  
  
 如果发出取消信号的标记与 <xref:System.Threading.Tasks.ParallelOptions> 实例中指定的标记相同，则并行循环将对取消引发单一 <xref:System.OperationCanceledException>。  如果某个其他标记导致取消，则循环将引发 <xref:System.AggregateException> 以及 <xref:System.OperationCanceledException> 作为 InnerException。  
  
## 请参阅  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)   
 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)