---
title: "Custom Partitioners for PLINQ and TPL | Microsoft Docs"
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
  - "tasks, partitioners"
ms.assetid: 96153688-9a01-47c4-8430-909cee9a2887
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Custom Partitioners for PLINQ and TPL
若要对数据源操作进行并行化，其中一个必要步骤是将源分区为可由多个线程同时访问的多个部分。  PLINQ 和任务并行库 \(TPL\) 提供了默认的分区程序，当您编写并行查询或 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 循环时，该分区程序将以透明方式工作。  对于更高级的方案，您可以插入自己的分区程序。  
  
## 分区的种类  
 可通过多种方法来对数据源进行分区。  在最有效的方法中，多个线程协同将处理原始源序列，而不是实际上将源划分为多个子序列。  对于数组和其他已建立索引的源（例如预先知道长度的 <xref:System.Collections.IList> 集合），按范围分区是最简单的分区种类。  每个线程都接收唯一的开始和结束索引，因此它能够处理其源范围，而不会覆盖任何其他线程或被任何其他线程覆盖。  按范围分区中涉及的唯一开销是创建范围的初始工作；之后不再需要其他同步。  因此，只要平均划分工作负载，它就能够提供很好的性能。  按范围分区的缺点是：如果一个线程提前完成，它将无法帮助其他线程完成它们的工作。  
  
 对于长度未知的链接列表或其他集合，您可以使用按区块分区。  在按区块分区中，并行循环或查询中的每个线程或任务都使用一个区块中一定数量的源元素，对它们进行处理，然后返回检索其他元素。  分区程序可确保分发所有元素，并且没有重复项。  区块可为任意大小。  例如，[How to: Implement Dynamic Partitions](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md) 中演示的分区程序将创建只包含一个元素的区块。  只要区块不是太大，这种分区在本质上是负载平衡的，原因是为线程分配元素的操作不是预先确定的。  但是，每次线程需要获取另一个区块时，分区程序都会产生同步开销。  在这些情况下产生的同步量与区块的大小成反比。  
  
 通常，只有当委托的执行时间为较短到中等程度，源具有大量的元素，并且每个分区的总工作量大致相等时，按范围分区的速度才会较快。  因此，按区块分区的速度在大多数情况下较快。  对于元素数量很少或委托执行时间较长的源，则按区块分区和按范围分区的性能大致相等。  
  
 TPL 分区程序还支持动态数量的分区。  这意味着，它们可以即时创建分区，举例来说，当 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 循环生成新任务时，情况即是如此。  此功能使分区程序能够随循环本身一起缩放。  动态分区程序在本质上也是负载平衡的。  当您创建自定义分区程序时，您必须支持可从 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 循环中使用动态分区。  
  
### 针对 PLINQ 配置负载平衡的分区程序  
 <xref:System.Collections.Concurrent.Partitioner.Create%2A?displayProperty=fullName> 方法的某些重载允许您为数组或 <xref:System.Collections.IList> 源创建分区程序，并指定其分区程序是否应尝试平衡线程之间的工作负载。  如果分区程序配置为负载平衡，则使用按区块分区，并根据元素请求将元素传递给小区块中的每个分区。  此方法可帮助确保在整个循环或查询完成之前所有分区都有要处理的元素。  还可以使用另一个重载来提供任何 <xref:System.Collections.IEnumerable> 源的负载平衡分区。  
  
 通常，负载平衡要求分区以相对频繁的方式从分区程序请求元素。  相比之下，执行静态分区的分区程序可通过使用按范围分区或按区块分区同时将元素分配给每个分区程序。  这种方式需要的开销比负载平衡少，但是，如果一个线程结束时的工作量明显比其他线程多，则这种方式的执行时间可能较长。  默认情况下，当传递 IList 或数组时，PLINQ 始终使用无负载平衡的按范围分区。  若要为 PLINQ 启用负载平衡，请使用 `Partitioner.Create` 方法，如下面的示例所示。  
  
 [!code-csharp[TPL_Partitioners#02](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioners.cs#02)]
 [!code-vb[TPL_Partitioners#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/partitionsnippets_vb.vb#02)]  
  
 确定在任何给定方案中是否使用负载平衡的最佳方式是：体验并度量操作在有代表性的负载和计算机配置下要花多长时间完成。  例如，静态分区在只有少量核心的多核计算机上的速度可能会明显加快，但在具有相对较多核心的计算机上则可能会导致速度下降。  
  
 下表列出了 <xref:System.Collections.Concurrent.Partitioner.Create%2A> 方法的可用重载。  这些分区程序并非只能用于 PLINQ 或 <xref:System.Threading.Tasks.Task>。  它们也可以用于任何自定义并行构造。  
  
|重载|使用负载平衡|  
|--------|------------|  
|<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>|始终|  
|[Create\<TSource\>\(TSource\<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28%60%600%5B%5D%2CSystem.Boolean%29>|将布尔型参数指定为 true 时|  
|<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28System.Collections.Generic.IList%7B%60%600%7D%2CSystem.Boolean%29>|将布尔型参数指定为 true 时|  
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int32%2CSystem.Int32%29>|从不|  
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int32%2CSystem.Int32%2CSystem.Int32%29>|从不|  
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int64%2CSystem.Int64%29>|从不|  
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int64%2CSystem.Int64%2CSystem.Int64%29>|从不|  
  
### 为 Parallel.ForEach 配置静态按范围分区程序  
 在 <xref:System.Threading.Tasks.Parallel.For%2A> 循环中，将以委托方式将循环的主体提供给方法。  调用该委托的开销大致与虚方法调用相同。  在某些情况下，并行循环的主体可能很小，导致对每个循环迭代的委托调用的开销变得很大。  在这些情况下，您可以使用 <xref:System.Collections.Concurrent.Partitioner.Create%2A> 重载之一来针对源元素创建范围分区的 <xref:System.Collections.Generic.IEnumerable%601>。  然后，您可以将此范围集合传递给其主体由常规 `for` 循环组成的 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 方法。  此方法的优点是：每个范围只会产生委托调用开销一次，而不是每个元素产生一次。  下面的示例演示基本模式。  
  
 [!code-csharp[TPL_Partitioners#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioner01.cs#01)]
 [!code-vb[TPL_Partitioners#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/partitionercreate01.vb#01)]  
  
 循环中的每个线程都接收其自己的 <xref:System.Tuple%602>，其中包含指定子范围中的起始和结束索引值。  内部 `for` 循环使用 `fromInclusive` 和 `toExclusive` 值来直接循环数组或 <xref:System.Collections.IList>。  
  
 利用 <xref:System.Collections.Concurrent.Partitioner.Create%2A> 重载之一，您可以指定分区大小以及分区数量。  在每个元素的工作量非常低以致于即使每个元素一个虚方法调用都会对性能产生显著影响的情况下，可以使用此重载。  
  
## 自定义分区程序  
 在某些情况下，可能值得或者甚至要求实现您自己的分区程序。  例如，您可能有这样一个自定义集合类，根据您对该类的内部结构的了解，您能够采用比默认分区程序更有效的方式对其进行分区。  或者，根据您对在源集合中的不同位置处理元素所花费时间的了解，您可能需要创建大小不同的范围分区。  
  
 若要创建基本自定义分区程序，请按下表中所述方式从 <xref:System.Collections.Concurrent.Partitioner%601?displayProperty=fullName> 派生一个类并重写虚方法。  
  
|||  
|-|-|  
|<xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>|此方法由主线程调用一次，并返回 IList\(IEnumerator\(TSource\)\)。  循环或查询中的每个工作线程都可对列表调用 `GetEnumerator`，针对不同的分区检索 <xref:System.Collections.Generic.IEnumerator%601>。|  
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|如果您实现 <xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A>，则返回 `true`，否则返回 `false`。|  
|<xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A>|如果 <xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A> 为 `true`，则可以选择调用此方法，而不是 <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>。|  
  
 如果结果必须可排序，或者您需要对元素的索引访问，则按下表中所述方式从 <xref:System.Collections.Concurrent.OrderablePartitioner%601?displayProperty=fullName> 派生并重写其虚方法。  
  
|||  
|-|-|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetPartitions%2A>|此方法由主线程调用一次，并返回 `IList(IEnumerator(TSource))`。  循环或查询中的每个工作线程都可对列表调用 `GetEnumerator`，针对不同的分区检索 <xref:System.Collections.Generic.IEnumerator%601>。|  
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|如果您实现 <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetDynamicPartitions%2A>，则返回 `true`；否则返回 false。|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetDynamicPartitions%2A>|通常，它只调用 <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A>。|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A>|如果 <xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A> 为 `true`，则可以选择调用此方法，而不是 <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>。|  
  
 下表提供了有关三种负载平衡分区程序如何实现 <xref:System.Collections.Concurrent.OrderablePartitioner%601> 类的其他详细信息。  
  
|方法\/属性|无负载平衡的 IList\/数组|带负载平衡的 IList\/数组|IEnumerable|  
|------------|----------------------|----------------------|-----------------|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A>|使用按范围分区|使用针对指定 partitionCount 的列表优化的按区块分区|通过创建静态数量的分区使用按区块分区。|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A?displayProperty=fullName>|引发不受支持异常|使用针对列表和动态分区优化的按区块分区|通过创建动态数量的分区使用按区块分区。|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysOrderedInEachPartition%2A>|返回 `true`|返回 `true`|返回 `true`|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysOrderedAcrossPartitions%2A>|返回 `true`|返回 `false`|返回 `false`|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysNormalized%2A>|返回 `true`|返回 `true`|返回 `true`|  
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|返回 `false`|返回 `true`|返回 `true`|  
  
### 动态分区  
 如果打算要在 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 方法中使用分区程序，您必须能够返回动态数量的分区。  这意味着，分区程序能够在循环执行过程中随时按需为新分区提供枚举器。  基本上，每当循环添加一个新并行任务时，它都会为该任务请求一个新分区。  如果要求数据可排序，则从 <xref:System.Collections.Concurrent.OrderablePartitioner%601?displayProperty=fullName> 派生，以便为每个分区中的每个项分配唯一的索引。  
  
 有关更多信息和示例，请参见[How to: Implement Dynamic Partitions](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md)。  
  
### 分区程序的协定  
 在实现自定义分区程序时，请遵循下列准则，以帮助确保与 PLINQ 和 TPL 中的 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 正确进行交互：  
  
-   如果使用等于零或小于零的 `partitionsCount` 参数调用 <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>，则会引发 <xref:System.ArgumentOutOfRangeException>。  尽管 PLINQ 和 TPL 将从不会传入等于 0 的 `partitionCount`，但我们仍然建议您防止这种可能性。  
  
-   <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A> 和 <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A> 应始终返回 `partitionsCount` 分区数。  如果分区程序的数据不足而无法按请求创建多个分区，则方法应为其余每个分区返回空枚举器。  否则，PLINQ 和 TPL 都将引发 <xref:System.InvalidOperationException>。  
  
-   <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>、<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A>、<xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A> 和 <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A> 决不应返回 `null` （Visual Basic 中为 `Nothing` ）。  如果它们返回了该值，则 PLINQ \/ TPL 将引发 <xref:System.InvalidOperationException>。  
  
-   返回分区的方法应始终返回可完全并唯一地枚举数据源的分区。  除非分区程序的设计特别要求，否则数据源或跳过的项中不应有重复项。  如果未遵循此规则，则输出顺序可能会混乱。  
  
-   下面的布尔型 getter 必须始终准确地返回以下值，以使输出顺序不会混乱：  
  
    -   `KeysOrderedInEachPartition`：每个分区返回具有不断增加的键索引的元素。  
  
    -   `KeysOrderedAcrossPartitions`：对于返回的所有分区，分区 *i* 中的键索引大于分区 *i*\-1 中的键索引。  
  
    -   `KeysNormalized`：所有键索引将从零开始单调递增（没有间隔）。  
  
-   所有索引必须唯一。  不能有重复索引。  如果未遵循此规则，则输出顺序可能会混乱。  
  
-   所有索引必须为非负。  如果未遵循此规则，则 PLINQ\/TPL 可能会引发异常。  
  
## 请参阅  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)   
 [How to: Implement Dynamic Partitions](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md)   
 [How to: Implement a Partitioner for Static Partitioning](../../../docs/standard/parallel-programming/how-to-implement-a-partitioner-for-static-partitioning.md)