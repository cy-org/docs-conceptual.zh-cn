---
title: "Order Preservation in PLINQ | Microsoft Docs"
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
  - "PLINQ queries, order preservation"
ms.assetid: 10d202bc-19e1-4b5c-bbf1-9a977322a9ca
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Order Preservation in PLINQ
在 PLINQ 中，目标是在保持正确性的同时最大程度地提升性能。  查询应尽快运行，但仍然应生成正确的结果。  在某些情况下，正确性要求源序列的顺序得以保留；但是，排序可能会消耗大量的计算资源。  因此，在默认情况下，PLINQ 不会保留源序列的顺序。  就这一点而言，PLINQ 类似于 [!INCLUDE[vbtecdlinq](../../../includes/vbtecdlinq-md.md)]，但与会保留排序的 LINQ to Objects 不同。  
  
 若要重写默认行为，您可以通过对源序列使用 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 运算符来启用顺序保留。  然后，您可以稍后通过使用 <xref:System.Linq.ParallelEnumerable.AsUnordered%2A> 方法在查询中禁用顺序保留。  对于这两个方法，将基于确定以并行还是顺序方式执行查询的探索处理查询。  有关详细信息，请参阅[Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)。  
  
 下面的示例演示一个未排序的并行查询，该查询筛选与某个条件匹配的所有元素，而不会尝试以任何方式对结果进行排序。  
  
 [!code-csharp[PLINQ#8](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#8)]
 [!code-vb[PLINQ#8](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#8)]  
  
 此查询不一定会生成源序列中满足条件的前 1000 个城市，而是会生成满足条件的某一组 1000 个城市。  PLINQ 查询运算符会将源序列分区为作为并发任务处理的多个子序列。  如果未指定顺序保留，则会按任意顺序将每个分区中的结果传递给查询的下一阶段。  此外，分区可能会在继续处理其余元素之前生成其结果的子集。  产生的顺序每次可能都不同。  您的应用程序无法控制这一点，因为它依赖于操作系统调度线程的方式。  
  
 下面的示例通过对源序列使用 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 运算符来重写默认行为。  这将确保 <xref:System.Linq.ParallelEnumerable.Take%2A> 方法返回源序列中满足条件的前 1000 个城市。  
  
 [!code-csharp[PLINQ#9](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#9)]
 [!code-vb[PLINQ#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#9)]  
  
 但是，此查询的运行速度可能不如未排序版本快，因为它必须在各个分区中跟踪原始排序，并在合并时确保排序是一致的。  因此，我们建议您仅在必需时才使用 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A>，并且仅为需要它的那些查询部分使用。  不再需要顺序保留时，请使用 <xref:System.Linq.ParallelEnumerable.AsUnordered%2A> 将其禁用。  下面的示例通过编写两个查询来实现这一点。  
  
 [!code-csharp[PLINQ#6](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#6)]
 [!code-vb[PLINQ#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#6)]  
  
 请注意，PLINQ 保留由查询其余部分的顺序限制运算符生成的序列排序。  换言之，诸如 <xref:System.Linq.ParallelEnumerable.OrderBy%2A> 和 <xref:System.Linq.ParallelEnumerable.ThenBy%2A> 等运算符将被视为好像在它们之后调用了 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A>。  
  
## 查询运算符和排序  
 下面的查询运算符将顺序保留引入查询的所有后续运算中，或直至调用 <xref:System.Linq.ParallelEnumerable.AsUnordered%2A> 为止：  
  
-   <xref:System.Linq.ParallelEnumerable.OrderBy%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.OrderByDescending%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.ThenBy%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.ThenByDescending%2A>  
  
 下面的 PLINQ 查询运算符在某些情况下可能要求经过排序的源序列生成正确的结果：  
  
-   <xref:System.Linq.ParallelEnumerable.Reverse%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.SequenceEqual%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.TakeWhile%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.SkipWhile%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.Zip%2A>  
  
 某些 PLINQ 查询运算符的行为有所不同，具体情况取决于其源序列是否已经过排序。  下表列出了这些运算符。  
  
|运算符|在源序列经过排序时生成|在源序列未经过排序时生成|  
|---------|-----------------|------------------|  
|<xref:System.Linq.ParallelEnumerable.Aggregate%2A>|不可结合或不可交换的操作的不确定输出|不可结合或不可交换的操作的不确定输出|  
|<xref:System.Linq.ParallelEnumerable.All%2A>|不适用|不适用|  
|<xref:System.Linq.ParallelEnumerable.Any%2A>|不适用|不适用|  
|<xref:System.Linq.ParallelEnumerable.AsEnumerable%2A>|不适用|不适用|  
|<xref:System.Linq.ParallelEnumerable.Average%2A>|不可结合或不可交换的操作的不确定输出|不可结合或不可交换的操作的不确定输出|  
|<xref:System.Linq.ParallelEnumerable.Cast%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.Concat%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.Count%2A>|不适用|不适用|  
|<xref:System.Linq.ParallelEnumerable.DefaultIfEmpty%2A>|不适用|不适用|  
|<xref:System.Linq.ParallelEnumerable.Distinct%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.ElementAt%2A>|返回指定的元素|任意元素|  
|<xref:System.Linq.ParallelEnumerable.ElementAtOrDefault%2A>|返回指定的元素|任意元素|  
|<xref:System.Linq.ParallelEnumerable.Except%2A>|未经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.First%2A>|返回指定的元素|任意元素|  
|<xref:System.Linq.ParallelEnumerable.FirstOrDefault%2A>|返回指定的元素|任意元素|  
|<xref:System.Linq.ParallelEnumerable.ForAll%2A>|以非确定性的方式并行执行|以非确定性的方式并行执行|  
|<xref:System.Linq.ParallelEnumerable.GroupBy%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.GroupJoin%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.Intersect%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.Join%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.Last%2A>|返回指定的元素|任意元素|  
|<xref:System.Linq.ParallelEnumerable.LastOrDefault%2A>|返回指定的元素|任意元素|  
|<xref:System.Linq.ParallelEnumerable.LongCount%2A>|不适用|不适用|  
|<xref:System.Linq.ParallelEnumerable.Min%2A>|不适用|不适用|  
|<xref:System.Linq.ParallelEnumerable.OrderBy%2A>|对序列重新排序|开始新的经过排序的节|  
|<xref:System.Linq.ParallelEnumerable.OrderByDescending%2A>|对序列重新排序|开始新的经过排序的节|  
|<xref:System.Linq.ParallelEnumerable.Range%2A>|不适用（与 <xref:System.Linq.ParallelEnumerable.AsParallel%2A> 相同的默认值）|不适用|  
|<xref:System.Linq.ParallelEnumerable.Repeat%2A>|不适用（与 <xref:System.Linq.ParallelEnumerable.AsParallel%2A> 相同的默认值）|不适用|  
|<xref:System.Linq.ParallelEnumerable.Reverse%2A>|反转|不执行任何操作|  
|<xref:System.Linq.ParallelEnumerable.Select%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.Select%2A>（已编制索引）|经过排序的结果|未经过排序的结果。|  
|<xref:System.Linq.ParallelEnumerable.SelectMany%2A>|经过排序的结果。|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.SelectMany%2A>（已编制索引）|经过排序的结果。|未经过排序的结果。|  
|<xref:System.Linq.ParallelEnumerable.SequenceEqual%2A>|经过排序的比较|未经过排序的比较|  
|<xref:System.Linq.ParallelEnumerable.Single%2A>|不适用|不适用|  
|<xref:System.Linq.ParallelEnumerable.SingleOrDefault%2A>|不适用|不适用|  
|<xref:System.Linq.ParallelEnumerable.Skip%2A>|跳过前 *n* 个元素|跳过任意 *n* 个元素|  
|<xref:System.Linq.ParallelEnumerable.SkipWhile%2A>|经过排序的结果。|不确定。  对当前的任意顺序执行 SkipWhile|  
|<xref:System.Linq.ParallelEnumerable.Sum%2A>|不可结合或不可交换的操作的不确定输出|不可结合或不可交换的操作的不确定输出|  
|<xref:System.Linq.ParallelEnumerable.Take%2A>|采用前 `n` 个元素|采用任意 `n` 个元素|  
|<xref:System.Linq.ParallelEnumerable.TakeWhile%2A>|经过排序的结果|不确定。  对当前的任意顺序执行 TakeWhile|  
|<xref:System.Linq.ParallelEnumerable.ThenBy%2A>|补充 `OrderBy`|补充 `OrderBy`|  
|<xref:System.Linq.ParallelEnumerable.ThenByDescending%2A>|补充 `OrderBy`|补充 `OrderBy`|  
|<xref:System.Linq.ParallelEnumerable.ToArray%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.ToDictionary%2A>|不适用|不适用|  
|<xref:System.Linq.ParallelEnumerable.ToList%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.ToLookup%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.Union%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.Where%2A>|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.Where%2A>（已编制索引）|经过排序的结果|未经过排序的结果|  
|<xref:System.Linq.ParallelEnumerable.Zip%2A>|经过排序的结果|未经过排序的结果|  
  
 不会主动对未经排序的结果进行随机排序；它们只是未应用任何特殊排序逻辑。  在某些情况下，未经排序的查询可以保留源序列的排序。  对于使用已编制索引的 Select 运算符的查询，PLINQ 保证输出元素将按索引增加的顺序出现，但不保证将哪个索引分配给哪个元素。  
  
## 请参阅  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)   
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)