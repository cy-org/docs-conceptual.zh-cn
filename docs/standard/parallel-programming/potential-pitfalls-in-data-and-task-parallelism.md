---
title: "Potential Pitfalls in Data and Task Parallelism | Microsoft Docs"
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
  - "parallel programming, pitfalls"
ms.assetid: 1e357177-e699-4b8f-9e49-56d3513ed128
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Potential Pitfalls in Data and Task Parallelism
在许多情况下，<xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> 和 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 可以显著提高普通顺序循环的性能。  但是，对循环进行并行化的工作增加了复杂性，可能会导致在顺序代码中不常见或根本不会遇到的问题。  本主题列出了一些要在编写并行循环时避免的做法。  
  
## 不要假定并行始终速度更快  
 在某些情况下，并行循环可能比顺序循环的运行速度慢。  基本经验法则是，具有很少迭代和快速用户委托的并行循环未必会快很多。  但是，由于性能中涉及到很多因素，因此我们建议您始终衡量实际结果。  
  
## 避免写入共享内存位置  
 在顺序代码中，从静态变量或类字段中读取或写入静态变量或类字段的情况很常见。  但是，每当多个线程同时访问此类变量时，都很有可能出现争用条件。  即使您可以使用锁来同步对变量的访问，同步开销也可能会对性能造成损害。  因此，我们建议您尽可能在并行循环中避免访问共享状态，或至少限制对共享状态的访问。  实现此目的最佳方式是使用 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> 和 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 的重载，它们使用 <xref:System.Threading.ThreadLocal%601?displayProperty=fullName> 变量在循环执行过程中存储线程本地状态。  有关更多信息，请参见[How to: Write a Parallel.For Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md)和[How to: Write a Parallel.ForEach Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-foreach-loop-with-thread-local-variables.md)。  
  
## 避免过度并行化  
 通过使用并行循环，将会产生对源集合进行分区和同步工作线程的开销。  计算机上的处理器数进一步限制了并行化的优点。  在仅仅一个处理器上运行多个主要进行计算的线程时，速度并不会得到提升。  因此，您必须小心不要对循环进行过度并行化。  
  
 在嵌套循环中，最有可能发生过度并行化的情况。  在多数情况下，除非满足以下一个或多个条件，否则最好仅对外部循环进行并行化：  
  
-   已经知道内部循环非常长。  
  
-   您正在每张订单上执行开销极大的计算。（示例中所示的操作开销不大。）  
  
-   已经知道目标系统具有足够的处理器来处理通过对 `cust.Orders` 查询进行并行化所产生的线程数。  
  
 在所有情况下，确定最佳查询形式的最好方法是测试并衡量。  
  
## 避免调用非线程安全方法  
 从并行循环中写入非线程安全实例方法可能会导致出现程序可能检测得到也可能检测不到的数据损坏，  还可能会导致异常。  在下面的示例中，多个线程将尝试同时调用 <xref:System.IO.FileStream.WriteByte%2A?displayProperty=fullName> 方法，这是类所不支持的。  
  
 [!code-csharp[TPL_Pitfalls#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_pitfalls/cs/pitfalls.cs#04)]
 [!code-vb[TPL_Pitfalls#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_pitfalls/vb/pitfalls_vb.vb#04)]  
  
## 仅调用线程安全方法  
 .NET Framework 中的大多数静态方法都是线程安全的，并且可同时从多个线程中调用。  但是，即使在这些情况下，所涉及到的同步也可能导致查询速度大幅减慢。  
  
> [!NOTE]
>  可通过在查询中插入某些对 <xref:System.Console.WriteLine%2A> 的调用来自己测试这一点。  尽管在用于演示目的的文档示例中使用了此方法，但除非必要，否则不要在并行循环中使用它。  
  
## 注意线程关联问题  
 某些技术（例如，单线程单元 \(STA\) 组件的 COM 互操作性、Windows 窗体以及 Windows Presentation Foundation \(WPF\)）有要求代码在特定线程上运行的线程关联限制。  例如，在 Windows 窗体和 WPF 中，只能在创建控件的线程上访问控件。  举例来说，这意味着，除非您将线程计划程序配置为仅将工作安排在 UI 线程上，否则将无法从并行循环中更新列表控件。  有关详细信息，请参阅[How to: Schedule Work on the User Interface \(UI\) Thread](../Topic/How%20to:%20Schedule%20Work%20on%20the%20User%20Interface%20\(UI\)%20Thread.md)。  
  
## 在由 Parallel.Invoke 调用的委托中等待时要小心  
 在某些情况下，任务并行库将对任务进行内联操作，这意味着它将在当前正在执行的线程上连续运行任务。（有关详细信息，请参阅 [Task Schedulers](../Topic/Task%20Schedulers.md)。）此性能优化在某些情况下可能会导致死锁。  例如，两个任务可能运行相同的委托代码，该代码在事件发生时发出信号，并等待另一个任务发出信号。  如果在相同线程上将第二个任务内联为第一个，并且第一个任务进入等待状态，则第二个任务将永远无法发出其事件信号。  为了避免发生这种情况，您可以在等待操作上指定超时，或使用显式线程构造函数来帮助确保一个任务无法阻止另一个任务。  
  
## 不要假定 ForEach、For 和 ForAll 的迭代始终并行执行  
 请务必谨记，<xref:System.Threading.Tasks.Parallel.For%2A>、<xref:System.Threading.Tasks.Parallel.ForEach%2A> 或 <xref:System.Linq.ParallelEnumerable.ForAll%2A> 循环中的个别迭代可以但不必并行执行。  因此，您应避免编写任何依赖于并行执行的正确性或依赖于按任何特定顺序执行迭代的代码。  例如，此代码有可能会死锁：  
  
 [!code-csharp[TPL_Pitfalls#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_pitfalls/cs/pitfalls.cs#01)]
 [!code-vb[TPL_Pitfalls#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_pitfalls/vb/pitfalls_vb.vb#01)]  
  
 在此示例中，一个迭代设置事件，而所有其他迭代则等待事件。  在事件设置迭代完成之前，任何等待迭代均无法完成。  但是，在事件设置迭代有机会执行之前，等待迭代可能会阻止用于执行并行循环的所有线程。  这将导致死锁 – 事件设置迭代将从不执行，并且等待迭代将从不觉醒。  
  
 具体而言，并行循环的一个迭代应从不等待循环的另一个迭代来继续执行。  如果并行循环决定按相反顺序安排迭代，则会发生死锁。  
  
## 避免在 UI 线程上执行并行循环  
 务必要使应用程序的用户界面 \(UI\) 保持响应状态。  如果操作包含足够的工作来保证并行化，则可能不应在 UI 线程上运行该操作。而是应卸载要在后台线程上运行的该操作。  例如，如果要使用并行循环来计算应随后呈现在 UI 控件中的某些数据，则应考虑在任务实例内执行循环，而不是直接在 UI 事件处理程序中执行循环。只有当核心计算完成后，您才应随后将 UI 更新封送回 UI 线程。  
  
 如果要在 UI 线程上运行并行循环，请小心避免从循环内更新 UI 控件。  如果尝试从在 UI 线程上执行的并行循环内更新 UI 控件，将可能会导致状态损坏、异常、更新延迟甚至死锁，具体情况视 UI 更新的调用方式而定。  在下面的示例中，并行循环将阻止它在其上执行的 UI 线程，直至所有迭代完成为止。  但是，如果循环的迭代在后台线程上运行（就像 <xref:System.Threading.Tasks.Parallel.For%2A> 可能进行的操作一样），对 Invoke 的调用可能会导致将消息提交到 UI 线程，并阻止等待对该消息进行处理。  由于 UI 线程被阻止运行 <xref:System.Threading.Tasks.Parallel.For%2A>，因此消息将永远无法得到处理，并且 UI 线程将死锁。  
  
 [!code-csharp[TPL_Pitfalls#02](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_pitfalls/cs/pitfalls.cs#02)]
 [!code-vb[TPL_Pitfalls#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_pitfalls/vb/pitfalls_vb.vb#02)]  
  
 下面的示例演示如何通过在任务实例内运行循环来避免死锁。  循环不会阻止 UI 线程，并且消息可得到处理。  
  
 [!code-csharp[TPL_Pitfalls#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_pitfalls/cs/pitfalls.cs#03)]
 [!code-vb[TPL_Pitfalls#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_pitfalls/vb/pitfalls_vb.vb#03)]  
  
## 请参阅  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)   
 [Potential Pitfalls with PLINQ](../../../docs/standard/parallel-programming/potential-pitfalls-with-plinq.md)   
 [并行编程模式：了解并使用 .NET Framework 4 应用并行模式](http://go.microsoft.com/fwlink/?LinkID=185142)