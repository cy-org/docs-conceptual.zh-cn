---
title: "Data Parallelism (Task Parallel Library) | Microsoft Docs"
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
  - "parallelism, data"
ms.assetid: 3f05f33f-f1da-4b16-81c2-9ceff1bef449
caps.latest.revision: 25
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 25
---
# Data Parallelism (Task Parallel Library)
*数据并行*指的是对源集合或数组的元素同时（即，并行）执行相同操作的场景。  在数据并行操作中，对源集合进行分区，以便多个线程能够同时在不同的网段上操作。  
  
 任务并行库 \(TPL\) 支持通过 <xref:System.Threading.Tasks.Parallel?displayProperty=fullName> 类实现的数据并行。  此类对 [for](../Topic/for%20\(C%23%20Reference\).md) 循环和 [foreach](../Topic/foreach,%20in%20\(C%23%20Reference\).md) 循环（Visual Basic 中的 `For` 和 `For Each`）提供了基于方法的并行执行。  你为 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> 或 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 循环编写的循环逻辑与编写连续循环的相似。  无需创建线程或列工作项。  在基本循环中，不需要加锁。  TPL 为你处理所有低级别的工作。  有关使用 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> 和 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 的详细信息，请下载文档[并行编程模式：了解并使用 .NET Framework 4 应用并行模式](http://www.microsoft.com/download/details.aspx?id=19222)。  下面的代码示例演示了一个简单的 `foreach` 循环及其并行等效项。  
  
> [!NOTE]
>  本文档使用 lambda 表达式在 TPL 中定义委托。  如果不熟悉 C\# 或 Visual Basic 中的 lambda 表达式，请参阅 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)。  
  
 [!code-csharp[TPL#20](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/tpl.cs#20)]
 [!code-vb[TPL#20](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/tpl_vb.vb#20)]  
  
 并行循环运行时，TPL 将数据源进行分区，以便该循环可以同时对多个部分进行作用。  在后台，任务计划程序基于系统资源和工作负荷来划分任务。  如有可能，如果工作负荷变得不平衡了，计划程序将重新分配多个线程与处理器之间的工作。  
  
> [!NOTE]
>  你也可以提供你自己的自定义分区程序或计划程序。  有关详细信息，请参阅 [Custom Partitioners for PLINQ and TPL](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md)和[Task Schedulers](../Topic/Task%20Schedulers.md)。  
  
 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> 和 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 方法都有多个过载，可让你停止或中断循环执行，监视其它线程上循环的状态，保持本地线程状态，完成本地线程对象，控制并发程度等等。  启用此功能的帮助器类型包括 <xref:System.Threading.Tasks.ParallelLoopState>、<xref:System.Threading.Tasks.ParallelOptions>、<xref:System.Threading.Tasks.ParallelLoopResult>、<xref:System.Threading.CancellationToken> 和 <xref:System.Threading.CancellationTokenSource>。  
  
 有关详细信息，请参阅[并行编程模式](http://go.microsoft.com/fwlink/p/?LinkId=265491)。  
  
 PLINQ 支持使用声明性或查询类语法的数据并行。  有关详细信息，请参阅[Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)。  
  
## 相关主题  
  
|标题|描述|  
|--------|--------|  
|[How to: Write a Simple Parallel.For Loop](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-for-loop.md)|描述如何编写遍历任何数组或可变址 <xref:System.Collections.Generic.IEnumerable%601> 源集合的 <xref:System.Threading.Tasks.Parallel.For%2A> 循环。|  
|[How to: Write a Simple Parallel.ForEach Loop](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-foreach-loop.md)|描述如何编写遍历任何 <xref:System.Collections.Generic.IEnumerable%601> 源集合的 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 循环。|  
|[How to: Stop or Break from a Parallel.For Loop](http://msdn.microsoft.com/zh-cn/de52e4f1-9346-4ad5-b582-1a4d54dc7f7e)|描述如何停止或中断并行循环，以便所有线程都获得该操作的通知。|  
|[How to: Write a Parallel.For Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md)|描述如何编写 <xref:System.Threading.Tasks.Parallel.For%2A> 循环，该循环中每个线程都维持有对其它任何线程不可见的私有变量，以及如何在循环完成时，同步所有线程的结果。|  
|[How to: Write a Parallel.ForEach Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-foreach-loop-with-thread-local-variables.md)|描述如何编写 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 循环，该循环中每个线程都维持有对其它任何线程不可见的私有变量，以及如何在循环完成时，同步所有线程的结果。|  
|[How to: Cancel a Parallel.For or ForEach Loop](../../../docs/standard/parallel-programming/how-to-cancel-a-parallel-for-or-foreach-loop.md)|描述如何通过使用 <xref:System.Threading.CancellationToken?displayProperty=fullName> 取消并行循环|  
|[How to: Speed Up Small Loop Bodies](../../../docs/standard/parallel-programming/how-to-speed-up-small-loop-bodies.md)|描述在循环主体极小时加快执行速度的方法。|  
|[Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)|提供任务并行库的概述。|  
|[Parallel Programming](../../../docs/standard/parallel-programming/index.md)|介绍.NET Framework 中的并行编程。|  
  
## 请参阅  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)