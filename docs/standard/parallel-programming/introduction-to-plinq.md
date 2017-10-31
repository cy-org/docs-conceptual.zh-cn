---
title: "Introduction to PLINQ | Microsoft Docs"
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
  - "PLINQ queries, introduction to"
ms.assetid: eaa720d8-8999-4eb7-8df5-3c19ca61cad0
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 22
---
# Introduction to PLINQ
## 什么是并行查询？  
 在 [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)] 中引入语言集成查询 \(LINQ\)。它以类型安全的方式为查询的任意 <xref:System.Collections.IEnumerable?displayProperty=fullName> 或 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> 数据源提供了统一模型。  LINQ to Objects 是针对内存中集合（如 <xref:System.Collections.Generic.List%601>）和数组运行的 LINQ 查询的名称。  本文假定您对 LINQ 有基本的了解。  有关详细信息，请参阅 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)。  
  
 并行 LINQ \(PLINQ\) 是 LINQ 模式的并行实现。  PLINQ 查询在许多方面类似于非并行 LINQ to Objects 查询。  与顺序 [!INCLUDE[vbteclinq](../../../includes/vbteclinq-md.md)] 查询一样，PLINQ 查询对任何内存中 <xref:System.Collections.IEnumerable> 或 <xref:System.Collections.Generic.IEnumerable%601> 数据源进行操作，并推迟执行，这意味着在枚举查询之前不会开始执行这些操作。  主要区别是 PLINQ 尝试充分利用系统中的所有处理器。  它利用所有处理器的方法是，将数据源分成片段，然后在多个处理器上对单独工作线程上的每个片段并行执行查询。  在许多情况下，并行执行意味着查询运行速度显著提高。  
  
 通过并行执行，PLINQ 通常只需向数据源添加 <xref:System.Linq.ParallelEnumerable.AsParallel%2A> 查询操作，即可在某些查询类型的旧版代码上获得显著的性能改进。  但是，并行可能引入其自己的复杂性，因此并非所有查询操作在 PLINQ 中都运行得更快。  事实上，并行降低了某些查询的速度。  因此，您应了解诸如排序等问题如何影响并行查询。  有关详细信息，请参阅 [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)。  
  
> [!NOTE]
>  本文档使用 lambda 表达式在 PLINQ 中定义委托。  如果您不熟悉 C\# 或 Visual Basic 中的 lambda 表达式，请参见 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)。  
  
 本文的其余部分将概述主 PLINQ 类，并讨论如何创建 PLINQ 查询。  每节包含指向更详细信息和代码示例的链接。  
  
## ParallelEnumerable 类  
 <xref:System.Linq.ParallelEnumerable?displayProperty=fullName> 类公开 PLINQ 的几乎所有功能。此类和 <xref:System.Linq?displayProperty=fullName> 命名空间类型的其余部分一起编译到 System.Core.dll 程序集中。  Visual Studio 中的默认 C\# 和 Visual Basic 项目都引用该程序集并导入该命名空间。  
  
 <xref:System.Linq.ParallelEnumerable> 包括 LINQ to Objects 支持的所有标准查询运算符的实现，虽然它不尝试并行化每个实现。  如果您不熟悉 [!INCLUDE[vbteclinq](../../../includes/vbteclinq-md.md)]，请参见 [Introduction to LINQ](../../../ocs/visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)。  
  
 除了标准查询运算符，<xref:System.Linq.ParallelEnumerable> 类还包含一组支持特定于并行执行的行为的方法。  下表中列出了这些特定于 PLINQ 的方法。  
  
|ParallelEnumerable 运算符|描述|  
|----------------------------|--------|  
|<xref:System.Linq.ParallelEnumerable.AsParallel%2A>|PLINQ 的入口点。  指定如果可能，应并行化查询的其余部分。|  
|<xref:System.Linq.ParallelEnumerable.AsSequential%2A>|指定查询的其余部分应像非并行 LINQ 查询一样按顺序运行。|  
|<xref:System.Linq.ParallelEnumerable.AsOrdered%2A>|指定 PLINQ 应保留查询的其余部分的源序列排序，直到例如通过使用 orderby（在 Visual Basic 中为 Order By）子句更改排序为止。|  
|<xref:System.Linq.ParallelEnumerable.AsUnordered%2A>|指定查询的其余部分的 PLINQ 不需要保留源序列的排序。|  
|<xref:System.Linq.ParallelEnumerable.WithCancellation%2A>|指定 PLINQ 应定期监视请求取消时提供的取消标记和取消执行的状态。|  
|<xref:System.Linq.ParallelEnumerable.WithDegreeOfParallelism%2A>|指定 PLINQ 应当用来并行化查询的处理器的最大数目。|  
|<xref:System.Linq.ParallelEnumerable.WithMergeOptions%2A>|提供有关 PLINQ 应当如何（如果可能）将并行结果合并回到使用线程上的一个序列的提示。|  
|<xref:System.Linq.ParallelEnumerable.WithExecutionMode%2A>|指定 PLINQ 应当如何并行化查询（即使默认行为是按顺序运行查询）。|  
|<xref:System.Linq.ParallelEnumerable.ForAll%2A>|多线程枚举方法，与循环访问查询结果不同，它允许在不首先合并回到使用者线程的情况下并行处理结果。|  
|<xref:System.Linq.ParallelEnumerable.Aggregate%2A> 重载|对于 PLINQ 唯一的重载，它启用对线程本地分区的中间聚合以及一个用于合并所有分区结果的最终聚合函数。|  
  
## 选择使用模型  
 当您编写查询时，通过在数据源上调用 <xref:System.Linq.ParallelEnumerable.AsParallel%2A?displayProperty=fullName> 扩展方法来选择使用 PLINQ，如下面的示例所示。  
  
 [!code-csharp[PLINQ#1](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinq2_cs.cs#1)]
 [!code-vb[PLINQ#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#1)]  
  
 <xref:System.Linq.ParallelEnumerable.AsParallel%2A> 扩展方法将后续查询运算符（在本例中为 `where` 和 `select`）绑定到 <xref:System.Linq.ParallelEnumerable?displayProperty=fullName> 实现。  
  
## 执行模式  
 默认情况下，PLINQ 是保守的。  在运行时，PLINQ 基础结构分析查询的总体结构。  如果查询速度可能因并行而提高，则 PLINQ 将源序列分为可同时运行的任务。  如果并行化查询不安全，则 PLINQ 只会按顺序运行查询。  如果 PLINQ 可以在可能昂贵的并行算法或成本较低的顺序算法之间进行选择，则默认情况下它选择顺序算法。  可以使用 <xref:System.Linq.ParallelEnumerable.WithExecutionMode%2A> 方法和 <xref:System.Linq.ParallelExecutionMode?displayProperty=fullName> 枚举来指示 PLINQ 选择并行算法。  这在当您通过测试和测量知道特定查询以并行方式执行得更快时非常有用。  有关详细信息，请参阅 [How to: Specify the Execution Mode in PLINQ](../../../docs/standard/parallel-programming/how-to-specify-the-execution-mode-in-plinq.md)。  
  
## 并行度  
 默认情况下，PLINQ 使用主机上的所有处理器，这些处理器的数量最多可达 64 个。  通过使用 <xref:System.Linq.ParallelEnumerable.WithDegreeOfParallelism%2A> 方法，可以指示 PLINQ 使用不多于指定数量的处理器。  这在当您要确保计算机上运行的其他进程收到一定的 CPU 时间量时非常有用。  下面的代码片段将查询限制为最多使用两个处理器。  
  
 [!code-csharp[PLINQ#5](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#5)]
 [!code-vb[PLINQ#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#5)]  
  
 在查询要执行大量非计算绑定工作（如文件 I\/O）的情况下，最好指定比计算机上的核心数大的并行度。  
  
## 已排序和未排序的并行查询  
 在某些查询中，查询运算符必须产生保留源序列排序的结果。  PLINQ 针对此目的提供了 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 运算符。  <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 与 <xref:System.Linq.ParallelEnumerable.AsSequential%2A> 不同。  仍以并行方式处理 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 序列，但对其结果进行缓冲和排序。  由于排序保留通常包含额外工作，因此处理 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 序列的速度可能比处理默认 <xref:System.Linq.ParallelEnumerable.AsUnordered%2A> 序列慢。  特定的已排序并行操作是否比操作的顺序版本更快取决于许多因素。  
  
 下面的代码示例演示如何选择使用排序保留。  
  
 [!code-csharp[PLINQ#3](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinq2_cs.cs#3)]
 [!code-vb[PLINQ#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#3)]  
  
 有关详细信息，请参阅 [Order Preservation in PLINQ](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md)。  
  
## 并行 vs. 顺序查询  
 某些操作要求按顺序提供源数据。  <xref:System.Linq.ParallelEnumerable> 查询运算符在必要时自动转换为顺序模式。  对于要求顺序执行的用户定义的查询运算符和用户委托，PLINQ 提供了 <xref:System.Linq.ParallelEnumerable.AsSequential%2A> 方法。  当您使用 <xref:System.Linq.ParallelEnumerable.AsSequential%2A> 时，查询中的所有后续运算符按顺序执行，直到再次调用 <xref:System.Linq.ParallelEnumerable.AsParallel%2A>。  有关详细信息，请参阅 [How to: Combine Parallel and Sequential LINQ Queries](../../../docs/standard/parallel-programming/how-to-combine-parallel-and-sequential-linq-queries.md)。  
  
## 合并查询结果的选项  
 PLINQ 查询并行执行时，从每个辅助线程得到的结果必须合并回到主线程上，以便由 `foreach` 循环（在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 中为 `For Each`）使用或插入到列表或数组中。  例如在某些情况下，最好指定特定类型的合并操作，以更快地开始产生结果。  为此，PLINQ 支持 <xref:System.Linq.ParallelEnumerable.WithMergeOptions%2A> 方法和 <xref:System.Linq.ParallelMergeOptions> 枚举。  有关详细信息，请参阅 [Merge Options in PLINQ](../../../docs/standard/parallel-programming/merge-options-in-plinq.md)。  
  
## ForAll 运算符  
 在顺序 [!INCLUDE[vbteclinq](../../../includes/vbteclinq-md.md)] 查询中，执行延迟到在 `foreach`（在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 中为 `For Each`）循环中枚举查询或通过调用方法（例如 <xref:System.Linq.ParallelEnumerable.ToList%2A>、<xref:System.Linq.ParallelEnumerable.ToArray%2A> 或 <xref:System.Linq.ParallelEnumerable.ToDictionary%2A>）枚举查询为止。  在 PLINQ 中，还可以使用 `foreach` 执行查询和循环访问结果。  但是，`foreach` 本身不会并行运行，因此，它需要将所有并行任务的输出合并回到该循环正在其上运行的线程中。  在 PLINQ 中，当必须保留查询结果的最终排序时，以顺序方式处理结果时，以及例如当为每个语句调用 `Console.WriteLine` 时，必须使用 `foreach`。  为了使不需要保留排序时以及结果的处理可自己并行化时更快地执行查询，请使用 <xref:System.Linq.ParallelEnumerable.ForAll%2A> 方法来执行 PLINQ 查询。  <xref:System.Linq.ParallelEnumerable.ForAll%2A> 不执行此最终合并步骤。  下面的代码示例演示如何使用 <xref:System.Linq.ParallelEnumerable.ForAll%2A> 方法。  <xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=fullName> 用于此处是因为它已优化，可以同时添加多个线程而无需尝试移除任何项。  
  
 [!code-csharp[PLINQ#4](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinq2_cs.cs#4)]
 [!code-vb[PLINQ#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#4)]  
  
 下面的插图显示了 `foreach` 与 <xref:System.Linq.ParallelEnumerable.ForAll%2A> 在查询执行方面的区别。  
  
 ![ForAll 与Foreach](../../../docs/standard/parallel-programming/media/vs-isvnt-allvseach.png "VS\_ISVNT\_ALLvsEACH")  
  
## 取消  
 PLINQ 在 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 中与取消类型集成在一起。（有关更多信息，请参见 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)。）因此，与顺序 LINQ to Objects 查询不同，可以取消 PLINQ 查询。  若要创建可取消的 PLINQ 查询，请在查询上使用 <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> 运算符并提供 <xref:System.Threading.CancellationToken> 实例作为参数。  如果标记上的 <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> 属性设置为 true，则 PLINQ 将会注意到它，并停止所有线程上的处理，然后引发 <xref:System.OperationCanceledException>。  
  
 在设置取消标记后，PLINQ 查询可能还可以继续处理一些元素。  
  
 为了提高响应速度，您还可以响应在长时间运行的用户委托中的取消请求。  有关详细信息，请参阅 [How to: Cancel a PLINQ Query](../../../docs/standard/parallel-programming/how-to-cancel-a-plinq-query.md)。  
  
## 异常  
 当 PLINQ 查询执行时，可能会同时从不同的线程引发多个异常。  此外，处理异常的代码可能与引发异常的代码处于不同的线程上。  PLINQ 使用 <xref:System.AggregateException> 类型封装由一个查询引发的所有异常，并将这些异常封送回到调用线程。  在调用线程上，只需要一个 try\-catch 块。  但是，您可以循环访问在 <xref:System.AggregateException> 中封装的所有异常，并捕捉任何可以安全恢复的异常。  在极少数的情况下，可能会引发一些未包装在 <xref:System.AggregateException> 中的异常，而且也不包装 <xref:System.Threading.ThreadAbortException>。  
  
 如果允许异常向上冒泡回到联接线程，则查询操作也许可以在引发异常后继续处理一些项目。  
  
 有关详细信息，请参阅 [How to: Handle Exceptions in a PLINQ Query](../../../docs/standard/parallel-programming/how-to-handle-exceptions-in-a-plinq-query.md)。  
  
## 自定义分区程序  
 在某些情况下，您可以通过编写利用源数据的某些特征的自定义分区程序来提高查询性能。  在查询中，自定义分区程序本身是查询的可枚举对象。  
  
 [!code-csharp[PLINQ#2](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinq2_cs.cs#2)]
 [!code-vb[PLINQ#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq3.vb#2)]  
  
 PLINQ 支持固定数量的分区（尽管在运行时数据为了负载平衡可能被重新动态分配到这些分区）。  <xref:System.Threading.Tasks.Parallel.For%2A> 和 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 仅支持动态分区，这意味着分区数在运行时会更改。  有关详细信息，请参阅 [Custom Partitioners for PLINQ and TPL](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md)。  
  
## 测量 PLINQ 性能  
 在很多情况下，可以并行化查询，但是设置并行查询的开销可能比获得的性能收益大。  如果查询不执行太多计算，或者数据源很小，则 PLINQ 查询可能比顺序 LINQ to Objects 查询慢。  您可以在 Visual Studio Team Server 中使用并行性能分析器比较各种查询的性能，查找处理瓶颈，以及确定您的查询是并行运行还是按顺序运行。  有关更多信息，请参见[并发可视化工具](../Topic/Concurrency%20Visualizer.md)和[How to: Measure PLINQ Query Performance](../../../docs/standard/parallel-programming/how-to-measure-plinq-query-performance.md)。  
  
## 请参阅  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)   
 [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)