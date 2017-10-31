---
title: "How to: Write a Parallel.ForEach Loop with Thread-Local Variables | Microsoft Docs"
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
  - "parallel foreach loop, how to use local state"
ms.assetid: 24b10041-b30b-45cb-aa65-66cf568ca76d
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# How to: Write a Parallel.ForEach Loop with Thread-Local Variables
下面的示例演示如何编写使用线程本地变量的 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 方法。  当 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 循环执行时，它会将其源集合划分为多个分区。  每个分区都将获得自己的“线程本地”变量的副本。  （术语“线程本地”在此处不太准确，因为在某些情况下两个分区可能在同一线程上运行。）  
  
 此示例中的代码和参数非常类似于对应的 <xref:System.Threading.Tasks.Parallel.For%2A> 方法。  有关详细信息，请参阅[How to: Write a Parallel.For Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md)。  
  
 若要在 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 循环中使用线程本地变量，你必须调用采用两个类型参数的方法重载之一。  第一个类型参数 `TSource` 指定源元素的类型，第二个类型参数 `TLocal` 指定线程本地变量的类型。  
  
## 示例  
 以下示例调用 <xref:System.Threading.Tasks.Parallel.ForEach%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%601%7D%2CSystem.Func%7B%60%600%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%601%2C%60%601%7D%2CSystem.Action%7B%60%601%7D%29?displayProperty=fullName> 重载以计算一百万个元素的数组的总和。  此重载具有四个参数：  
  
-   `source`，也就是数据源。  它必须实现 <xref:System.Collections.Generic.IEnumerable%601>。  在我们的示例中，数据源是由 <xref:System.Linq.Enumerable.Range%2A?displayProperty=fullName> 方法返回的一百万个成员 `IEnumerable<Int32>` 对象。  
  
-   `localInit`，或初始化线程本地变量的函数。  为每个在其中执行 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 操作的分区调用此函数一次。  我们的示例将线程本地变量初始化为零。  
  
-   `body`，由并行循环对循环的每个迭代调用的 <xref:System.Func%604>。  其签名为 `Func\<TSource, ParallelLoopState, TLocal, TLocal>`。  你为委托提供代码，并且循环将传入输入参数，它们是：  
  
    -   <xref:System.Collections.Generic.IEnumerable%601> 的当前元素。  
  
    -   你可以在委托的代码中用来检查循环状态的 <xref:System.Threading.Tasks.ParallelLoopState> 变量。  
  
    -   线程本地变量。  
  
     你的委托返回线程本地变量，然后将此变量传递到在该特定分区中执行的循环的下一次迭代。  每个循环分区维护此变量的一个单独实例。  
  
     在该示例中，委托将每个整数的值添加到线程本地变量，该变量维护在该分区中整数元素的值的运行总数。  
  
-   `localFinally`，当在每个分区中的循环操作完成时，<xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 调用的 `Action<TLocal>` 委托。  <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 方法将为此线程（或循环分区）的线程本地变量的最终值传递给你的 `Action<TLocal>` 委托，并且你提供代码，这些代码执行将来自此分区的结果与其他分区的结果组合所需的操作。  此委托可以由多个任务并行调用。  因此，该示例使用 <xref:System.Threading.Interlocked.Add%28System.Int32%40%2CSystem.Int32%29?displayProperty=fullName> 方法以同步对 `total` 变量的访问。  由于委托类型为 <xref:System.Action%601>，因此不存在返回值。  
  
 [!code-csharp[TPL_Parallel#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/foreachthreadlocal.cs#04)]
 [!code-vb[TPL_Parallel#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/foreachthreadlocal.vb#04)]  
  
## 请参阅  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)   
 [How to: Write a Parallel.For Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md)   
 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)