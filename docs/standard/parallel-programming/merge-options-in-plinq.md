---
title: "Merge Options in PLINQ | Microsoft Docs"
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
  - "PLINQ queries, merge options"
ms.assetid: e8f7be3b-88de-4f33-ab14-dc008e76c1ba
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Merge Options in PLINQ
当查询以并行方式执行时，PLINQ 对源序列分区，以便多个线程可以并发处理通常在不同的线程上的不同部分。  例如，如果要在 `foreach`（在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 中为 `For Each`）循环中的一个线程上使用这些结果，则每个线程上返回的结果必须合并回一个序列。  PLINQ 执行的合并种类取决于查询中存在的运算符。  例如，对结果应用新顺序的运算符必须缓冲所有线程中的所有元素。  从使用线程的角度（这也是应用程序用户的角度）来看，完全缓冲的查询在生成其第一个结果之前，可能已运行了相当长的一段时间。  默认情况下，其他运算符部分缓冲；它们以批处理的方式生成其结果。  默认情况下，不缓冲运算符 <xref:System.Linq.ParallelEnumerable.ForAll%2A>。  它立即从所有线程生成所有元素。  
  
 如下面的示例所示，通过使用 <xref:System.Linq.ParallelEnumerable.WithMergeOptions%2A> 方法，可以向 PLINQ 提供一个提示，以指示要执行的合并种类。  
  
 [!code-csharp[PLINQ#26](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#26)]
 [!code-vb[PLINQ#26](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#26)]  
  
 有关完整的示例，请参见[How to: Specify Merge Options in PLINQ](../../../docs/standard/parallel-programming/how-to-specify-merge-options-in-plinq.md)。  
  
 如果特定的查询不支持请求的选项，将只忽略该选项。  在大多数情况下，不必为 PLINQ 查询指定合并选项。  然而，在某些情况下，您通过测试和测量会发现，查询最适合在非默认模式下执行。  此选项的一个常见用途是强制块区合并运算符流式处理其结果，以提供更具有响应能力的用户界面。  
  
## ParallelMergeOptions  
 <xref:System.Linq.ParallelMergeOptions> 枚举包括下列选项，这些选项为支持的查询形状指定当在一个线程上使用结果时如何生成查询的最终的输出：  
  
-   `Not Buffered`  
  
     通过 <xref:System.Linq.ParallelMergeOptions> 选项，每个处理的元素在生成后即从每个线程返回。  此行为类似于“流式处理”输出。  如果查询中存在 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 运算符，则 `NotBuffered` 保留源元素的顺序。  尽管 `NotBuffered` 一旦结果可用即开始产生结果，但生成所有结果的总时间仍可能比使用其他一个合并选项的时间长。  
  
-   `Auto Buffered`  
  
     通过<xref:System.Linq.ParallelMergeOptions> 选项，查询将元素收集到缓冲区中，并定期一次性将所有缓冲内容生成到使用线程中。  这类似于以“块”的形式而不是使用 `NotBuffered` 的“流式处理”行为来生成源数据。  `AutoBuffered` 可能花费比 `NotBuffered` 更长的时间以使第一个元素在使用线程上可用。  缓冲区的大小和准确的生成行为是不可配置的，且可能因与查询相关的各种因素而有所不同。  
  
-   `FullyBuffered`  
  
     通过 <xref:System.Linq.ParallelMergeOptions> 选项，在生成任何元素之前缓存整个查询的输出。  当您使用此选项时，第一个元素在使用线程上可用之前花费的时间比使用其他选项长，但产生完整结果的速度仍可能比使用其他选项快。  
  
## 支持合并选项的查询运算符  
 下表列出了支持所有合并选项模式的运算符，以及所受的指定限制。  
  
|运算符|限制|  
|---------|--------|  
|<xref:System.Linq.ParallelEnumerable.AsEnumerable%2A>|无|  
|<xref:System.Linq.ParallelEnumerable.Cast%2A>|无|  
|<xref:System.Linq.ParallelEnumerable.Concat%2A>|只有 Array 或 List 源的未排序查询。|  
|<xref:System.Linq.ParallelEnumerable.DefaultIfEmpty%2A>|无|  
|<xref:System.Linq.ParallelEnumerable.OfType%2A>|无|  
|<xref:System.Linq.ParallelEnumerable.Reverse%2A>|只有 Array 或 List 源的未排序查询。|  
|<xref:System.Linq.ParallelEnumerable.Select%2A>|无|  
|<xref:System.Linq.ParallelEnumerable.SelectMany%2A>|无|  
|<xref:System.Linq.ParallelEnumerable.Skip%2A>|无|  
|<xref:System.Linq.ParallelEnumerable.Take%2A>|无|  
|<xref:System.Linq.ParallelEnumerable.Where%2A>|无|  
  
 所有其他 PLINQ 查询运算符可能忽略用户提供的合并选项。  某些查询运算符（例如 <xref:System.Linq.ParallelEnumerable.Reverse%2A> 和 <xref:System.Linq.ParallelEnumerable.OrderBy%2A>）在生成并重新排序所有元素之前，不会产生任何元素。  因此，如果在同样包含运算符（如 <xref:System.Linq.ParallelEnumerable.Reverse%2A>）的查询中使用 <xref:System.Linq.ParallelMergeOptions>，则在该运算符生成其结果之前，查询中不会应用合并行为。  
  
 某些运算符处理合并选项的能力取决于源序列的类型以及以前是否在查询中使用了 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 运算符。  <xref:System.Linq.ParallelEnumerable.ForAll%2A> 始终为 <xref:System.Linq.ParallelMergeOptions>；它立即生成其元素。  <xref:System.Linq.ParallelEnumerable.OrderBy%2A> 始终为 <xref:System.Linq.ParallelMergeOptions>；它必须在生成前对整个列表进行排序。  
  
## 请参阅  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)   
 [How to: Specify Merge Options in PLINQ](../../../docs/standard/parallel-programming/how-to-specify-merge-options-in-plinq.md)