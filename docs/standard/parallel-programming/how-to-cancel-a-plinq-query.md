---
title: "How to: Cancel a PLINQ Query | Microsoft Docs"
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
  - "PLINQ queries, how to cancel"
  - "cancellation, PLINQ"
ms.assetid: 80b14640-edfa-4153-be1b-3e003d3e9c1a
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# How to: Cancel a PLINQ Query
下面的示例演示取消 PLINQ 查询的两种方式。  第一个示例演示如何取消主要由数据遍历组成的查询。  第二个示例演示如何取消其中包含需要消耗大量计算资源的用户函数的查询。  
  
> [!NOTE]
>  当启用“仅我的代码”时，Visual Studio 将在引发异常的行上中断运行，并显示错误消息“异常未由用户代码处理”。此错误是良性的。  可以按 F5 从中断处继续运行，并查看在以下示例中演示的异常处理行为。  若要阻止 Visual Studio 在出现第一个错误时中断运行，只需在**“工具”\-\>“选项”\-\>“调试”\-\>“常规”**下取消选中“仅我的代码”复选框即可。  
>   
>  本示例旨在演示用法，运行速度可能不如等效的顺序 LINQ to Objects 查询快。  有关加速的更多信息，请参见[Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)。  
  
## 示例  
 [!code-csharp[PLINQ#16](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#16)]
 [!code-vb[PLINQ#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#16)]  
  
 PLINQ 框架不会将单一 <xref:System.OperationCanceledException> 滚入 <xref:System.AggregateException?displayProperty=fullName>；必须在单独的 catch 块中处理 <xref:System.OperationCanceledException>。  如果一个或多个用户委托（通过使用外部 <xref:System.Threading.CancellationToken?displayProperty=fullName>）引发 OperationCanceledException\(externalCT\)，但未引发其他异常，并且查询定义为 `AsParallel().WithCancellation(externalCT)`，则 PLINQ 将发出单一 <xref:System.OperationCanceledException> \(externalCT\)，而不是 <xref:System.AggregateException?displayProperty=fullName>。  但是，如果一个用户委托引发 <xref:System.OperationCanceledException>，而另一个用户委托引发另一种异常类型，则两个异常都将滚入 <xref:System.AggregateException>。  
  
 有关取消的一般性指导原则如下所示：  
  
1.  如果执行用户委托取消，则应将外部 <xref:System.Threading.CancellationToken> 告知 PLINQ，并引发 <xref:System.OperationCanceledException>\(externalCT\)。  
  
2.  如果进行取消并且未引发其他异常，则您应处理 <xref:System.OperationCanceledException>，而不是 <xref:System.AggregateException>。  
  
## 示例  
 下面的示例演示当用户代码中有需要消耗大量计算资源的函数时如何处理取消。  
  
 [!code-csharp[PLINQ#17](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#17)]
 [!code-vb[PLINQ#17](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#17)]  
  
 当您在用户代码中处理取消时，不必在查询定义中使用 <xref:System.Linq.ParallelEnumerable.WithCancellation%2A>。  但是，我们建议您这样做，原因是 <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> 对查询性能没有影响，并且它使取消能够由查询运算符和用户代码进行处理。  
  
 为了确保系统响应能力，我们建议您大约每毫秒检查是否存在取消一次；不过，任何 10 毫秒以下的期间都被视为可接受。  此频率对代码的性能应没有负面影响。  
  
 在释放枚举器时，例如，当代码中断循环访问查询结果的 foreach（在 Visual Basic 中为 For Each）循环时，将会取消查询，但不会引发异常。  
  
## 请参阅  
 <xref:System.Linq.ParallelEnumerable>   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)   
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)