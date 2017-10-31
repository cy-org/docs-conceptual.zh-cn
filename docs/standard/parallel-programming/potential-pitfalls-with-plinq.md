---
title: "Potential Pitfalls with PLINQ | Microsoft Docs"
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
  - "PLINQ queries, pitfalls"
ms.assetid: 75a38b55-4bc4-488a-87d5-89dbdbdc76a2
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Potential Pitfalls with PLINQ
在很多情况下，PLINQ 能够显著改进顺序 LINQ to Objects 查询的性能。  但是，对查询执行进行并行化的工作增加了复杂性，可能会导致在顺序代码中不常见或根本不会遇到的问题。  本主题列出了一些要在编写 PLINQ 查询时避免的做法。  
  
## 不要假定并行始终速度更快  
 并行化有时会导致 PLINQ 查询比其 LINQ to Objects 等效项运行更慢。  基本经验法则是，具有很少源元素和快速用户委托的查询未必会快很多。  但是，由于性能中涉及到很多因素，因此我们建议您在决定是否使用 PLINQ 之前衡量实际结果。  有关详细信息，请参阅[Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)。  
  
## 避免写入共享内存位置  
 在顺序代码中，从静态变量或类字段中读取或写入静态变量或类字段的情况很常见。  但是，每当多个线程同时访问此类变量时，都很有可能出现争用条件。  即使您可以使用锁来同步对变量的访问，同步开销也可能会对性能造成损害。  因此，我们建议您尽可能在 PLINQ 查询中避免访问共享状态，或至少限制对共享状态的访问。  
  
## 避免过度并行化  
 通过使用 `AsParallel` 运算符，将会产生对源集合进行分区和同步辅助线程的开销。  计算机上的处理器数进一步限制了并行化的优点。  在仅仅一个处理器上运行多个主要进行计算的线程时，速度并不会得到提升。  因此，您必须小心不要对查询进行过度并行化。  
  
 在嵌套查询中，最有可能发生过度并行化的情况，如下面的代码段所示。  
  
 [!code-csharp[PLINQ#20](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#20)]
 [!code-vb[PLINQ#20](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#20)]  
  
 在这种情况下，除非满足以下一个或多个条件，否则最好仅对外部数据源 \(customers\) 进行并行化：  
  
-   已经知道内部数据源 \(cust.Orders\) 非常长。  
  
-   您正在每张订单上执行开销极大的计算。（示例中所示的操作开销不大。）  
  
-   已经知道目标系统具有足够的处理器来处理通过对 `cust.Orders` 查询进行并行化所产生的线程数。  
  
 在所有情况下，确定最佳查询形式的最好方法是测试并衡量。  有关详细信息，请参阅[How to: Measure PLINQ Query Performance](../../../docs/standard/parallel-programming/how-to-measure-plinq-query-performance.md)。  
  
## 避免调用非线程安全方法  
 从 PLINQ 查询中写入非线程安全实例方法可能会导致出现程序可能检测得到也可能检测不到的数据损坏，  还可能会导致异常。  在下面的示例中，多个线程将尝试同时调用 `Filestream.Write` 方法，这是类所不支持的。  
  
```vb  
Dim fs As FileStream = File.OpenWrite(…)  
a.Where(...).OrderBy(...).Select(...).ForAll(Sub(x) fs.Write(x))  
```  
  
```csharp  
FileStream fs = File.OpenWrite(...);  
a.Where(...).OrderBy(...).Select(...).ForAll(x => fs.Write(x));  
```  
  
## 仅调用线程安全方法  
 .NET Framework 中的大多数静态方法都是线程安全的，并且可同时从多个线程中调用。  但是，即使在这些情况下，所涉及到的同步也可能导致查询速度大幅减慢。  
  
> [!NOTE]
>  可通过在查询中插入某些对 <xref:System.Console.WriteLine%2A> 的调用来自己测试这一点。  尽管用于演示用途的文档示例中使用了此方法，但不要在 PLINQ 查询中使用它。  
  
## 避免不必要的排序操作  
 当 PLINQ 以并行方式执行查询时，它会将源序列划分为可同时在多个线程上操作的多个分区。  默认情况下，处理这些分区和提供结果时采用的顺序是不可预测的（但诸如 `OrderBy` 等运算符除外）。  您可以指示 PLINQ 保留任何源序列的顺序，但这样会对性能产生负面影响。  只要有可能，最佳做法是构造查询以使它们不依赖于顺序保留。  有关详细信息，请参阅[Order Preservation in PLINQ](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md)。  
  
## 尽可能首选使用 ForAll，而非 ForEach  
 尽管 PLINQ 在多个线程上执行查询，但如果您使用 `foreach` 循环（Visual Basic 中为 `For Each`）中的结果，则必须将查询结果合并回一个线程中，并由枚举器依次访问。  在某些情况下，这是不可避免的；但是，请尽可能使用 `ForAll` 方法使每个线程都能够输出其自己的结果，例如，通过写入诸如 <xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=fullName> 等线程安全集合。  
  
 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 也有同样的问题,换言之，强烈建议应首选使用 `source.AsParallel().Where().ForAll(...)`  
  
 `Parallel.ForEach(source.AsParallel().Where(), ...)`.  
  
## 注意线程关联问题  
 某些技术（例如，单线程单元 \(STA\) 组件的 COM 互操作性、Windows 窗体以及 Windows Presentation Foundation \(WPF\)）有要求代码在特定线程上运行的线程关联限制。  例如，在 Windows 窗体和 WPF 中，只能在创建控件的线程上访问控件。  如果尝试在 PLINQ 查询中访问 Windows 窗体控件的共享状态，则在调试器中运行的情况下会引发异常。（可禁用此设置。）但是，如果在 UI 线程上使用您的查询，则可以从枚举查询结果的 `foreach` 循环中访问控件，因为该代码仅在一个线程上执行。  
  
## 不要假定 ForEach、For 和 ForAll 的迭代始终并行执行  
 请务必谨记，<xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName>、<xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 或 <xref:System.Linq.ParallelEnumerable.ForAll%2A> 循环中的个别迭代可以但不必并行执行。  因此，您应避免编写任何依赖于并行执行的正确性或依赖于按任何特定顺序执行迭代的代码。  
  
 例如，此代码有可能会死锁：  
  
```vb  
Dim mre = New ManualResetEventSlim()  
    Enumerable.Range(0, ProcessorCount * 100).AsParallel().ForAll(Sub(j)   
  
                                                     If j = Environment.ProcessorCount Then  
  
                                                         Console.WriteLine("Set on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j)  
                                                         mre.Set()  
  
                                                     Else  
  
                                                         Console.WriteLine("Waiting on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j)  
                                                         mre.Wait()  
                                                     End If  
    End Sub) ' deadlocks  
```  
  
```csharp  
ManualResetEventSlim mre = new ManualResetEventSlim();  
            Enumerable.Range(0, ProcessorCount * 100).AsParallel().ForAll((j) =>  
            {  
                if (j == Environment.ProcessorCount)  
                {  
                    Console.WriteLine("Set on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j);  
                    mre.Set();  
                }  
                else  
                {  
                    Console.WriteLine("Waiting on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j);  
                    mre.Wait();  
                }  
            }); //deadlocks  
```  
  
 在此示例中，一个迭代设置事件，而所有其他迭代则等待事件。  在事件设置迭代完成之前，任何等待迭代均无法完成。  但是，在事件设置迭代有机会执行之前，等待迭代可能会阻止用于执行并行循环的所有线程。  这将导致死锁 – 事件设置迭代将从不执行，并且等待迭代将从不觉醒。  
  
 具体而言，并行循环的一个迭代应从不等待循环的另一个迭代来继续执行。  如果并行循环决定按相反顺序安排迭代，则会发生死锁。  
  
## 请参阅  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)