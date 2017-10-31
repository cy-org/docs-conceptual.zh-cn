---
title: "Understanding Speedup in PLINQ | Microsoft Docs"
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
  - "PLINQ queries, performance tuning"
ms.assetid: 53706c7e-397d-467a-98cd-c0d1fd63ba5e
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Understanding Speedup in PLINQ
PLINQ 的主要用途是通过在多核计算机上以并行方式执行查询委托来加快 LINQ to Objects 查询的执行速度。  当源集合中的每个元素的处理独立进行，各个委托之间未涉及到共享状态时，PLINQ 的性能最佳。  此类操作在 LINQ to Objects 和 PLINQ 中很常见，并且，由于这些操作有助于轻松地针对多个线程进行计划，因此通常称为“适合并行”。  但是，并非所有查询都完全由适合并行操作组成；大多数情况下，查询包含某些无法进行并行化或会减慢并行执行速度的运算符。  并且，即使对于完全适合并行的查询，PLINQ 也仍然必须对数据源进行分区并针对线程安排工作，并通常在查询完成时合并结果。  所有这些操作都会增加并行化的计算成本；这些增加并行化的成本称为“开销”。  若要在 PLINQ 查询中实现最佳性能，目标是最大程度地增加适合并行的部件，并最大程度地减少需要开销的部件。  本文提供的信息可帮助您编写尽可能高效而同时仍然能产生正确结果的 PLINQ 查询。  
  
## 影响 PLINQ 查询性能的因素  
 以下各节列出了会对并行查询性能产生影响的一些最重要的因素。  这些信息是概括性叙述，仅凭这些信息无法预测所有情况下的查询性能。  一直以来，衡量具有各种代表性配置和负载的计算机上特定查询的实际性能都十分重要。  
  
1.  总体工作的计算开销。  
  
     为了实现加速，PLINQ 查询必须具有足够的适合并行工作来弥补开销。  工作可表示为每个委托的计算开销与源集合中元素数量的乘积。  假定某个操作可并行化，则它的计算开销越高，加速的可能性就越大。  例如，如果某个函数执行花费的时间为 1 毫秒，则针对 1000 个元素进行的顺序查询将花费 1 秒来执行该操作，而在四核计算机上进行的并行查询可能只花费 250 毫秒。  这样就产生了 750 毫秒的加速。  如果该函数对于每个元素需要花费 1 秒来执行，则加速将为 750 秒。  如果委托的开销很大，则对于源集合中的很少几个项，PLINQ 可能会提供明显的加速。  相反，包含无关紧要委托的小型源集合通常不适合于 PLINQ。  
  
     在下面的示例中，queryA是 PLINQ 的理想候选项，假设其 Select 函数涉及大量工作。queryB 可能不是个理想的候选项，原因是 Select 语句中没有足够的工作，并且并行化开销将抵销大部分或全部加速。  
  
    ```vb  
    Dim queryA = From num In numberList.AsParallel()  
                 Select ExpensiveFunction(num); 'good for PLINQ  
  
    Dim queryB = From num In numberList.AsParallel()  
                 Where num Mod 2 > 0  
                 Select num; 'not as good for PLINQ  
    ```  
  
    ```csharp  
    var queryA = from num in numberList.AsParallel()  
                 select ExpensiveFunction(num); //good for PLINQ  
  
    var queryB = from num in numberList.AsParallel()  
                 where num % 2 > 0  
                 select num; //not as good for PLINQ  
  
    ```  
  
2.  系统上的逻辑内核数（并行度）。  
  
     这一点是前一节显而易见的必然结果，适合并行的查询在具有更多内核的计算机上运行更快，原因是可以在更多并行线程之间分担工作。  加速的总量取决于查询的总体工作中可并行化的百分比。  但是，请不要假定所有查询在八核计算机上的运行速度都比在四核计算机的运行速度快两倍。  在调整查询以实现最佳性能时，衡量具有多个内核的计算机上的实际结果十分重要。  这一点与第一点相关：更大的数据集需要消耗更多的计算资源。  
  
3.  操作的数量和种类。  
  
     对于必须要保持元素在源序列中的顺序的情况，PLINQ 提供了 AsOrdered 运算符。  排序会产生开销，但此开销通常是适度的。  GroupBy 和 Join 操作同样也会产生开销。  如果允许按任意顺序处理源集合中的元素，并在这些元素就绪时立即将它们传递到下一个运算符，则 PLINQ 的性能最佳。  有关详细信息，请参阅[Order Preservation in PLINQ](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md)。  
  
4.  查询的执行形式。  
  
     如果要通过调用 ToArray 或 ToList 存储查询的结果，则必须将来自所有并行线程的结果合并为单个数据结构。  这会涉及到不可避免的计算开销。  同样，如果您使用 foreach（Visual Basic 中为 For Each）循环对结果进行迭代，则需要将来自工作线程的结果序列化到枚举器线程上。  但是，如果只需要基于来自每个线程的结果执行某个操作，您可以使用 ForAll 方法在多个线程上执行此工作。  
  
5.  合并选项的类型。  
  
     可将 PLINQ 配置为将其输出放入缓冲区，并以区块方式或在整个结果集完成后同时生成输出，或者在个别结果生成时流式传送这些结果。  前者可缩短总体执行时间，而后者可缩短生成的元素之间的延迟。尽管合并选项并不总是对总体查询性能有很大影响，但是，由于它们控制用户必须等待多长时间才能看到结果，因此可能会对感觉到的性能产生影响。  有关详细信息，请参阅[Merge Options in PLINQ](../../../docs/standard/parallel-programming/merge-options-in-plinq.md)。  
  
6.  分区的种类。  
  
     在某些情况下，针对可建立索引的源集合进行的 PLINQ 查询可能会产生不平衡的工作负载。  如果发生这种情况，您也许能够通过创建自定义分区程序来提高查询性能。  有关详细信息，请参阅[Custom Partitioners for PLINQ and TPL](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md)。  
  
## PLINQ 何时选择顺序模式  
 PLINQ 将始终尝试至少按与查询以顺序方式运行同样的速度来执行查询。  尽管 PLINQ 不会查看用户委托的计算开销有多高或输入源有多大，但它却会查找某些查询“形状”。具体而言，它将查找通常会导致查询在并行模式下运行更慢的查询运算符或运算符组合。  如果找到此类形状，PLINQ 默认情况下会转而使用顺序模式。  
  
 但是，在衡量特定查询的性能后，您可能会确定该查询在并行模式下实际运行更快。  在这些情况下，您可以通过 <xref:System.Linq.ParallelEnumerable.WithExecutionMode%2A?displayProperty=fullName> 方法使用 <xref:System.Linq.ParallelExecutionMode> 标志，以指示 PLINQ 对查询进行并行化。  有关详细信息，请参阅[How to: Specify the Execution Mode in PLINQ](../../../docs/standard/parallel-programming/how-to-specify-the-execution-mode-in-plinq.md)。  
  
 下面的列表介绍了 PLINQ 默认情况下将按顺序模式执行的查询形状：  
  
-   包含 Select 子句、已建立索引的 Where 子句、已建立索引的 SelectMany 子句或 ElementAt 子句的查询（在排序或筛选运算符移除或重新排列了索引后）。  
  
-   包含 Take、TakeWhile、Skip、SkipWhile 运算符并且源序列中的索引未采用原始顺序的查询。  
  
-   包含 Zip 或 SequenceEquals 的查询，除非其中一个数据源具有按原始顺序排列的索引，并且另一个数据源可建立索引 \(例如：数组 或 IList\(T\)\).  
  
-   包含 Concat 的查询，除非将其应用到可建立索引的数据源。  
  
-   包含 Reverse 的查询，除非应用到可建立索引的数据源。  
  
## 请参阅  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)