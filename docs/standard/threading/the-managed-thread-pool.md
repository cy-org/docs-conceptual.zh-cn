---
title: "The Managed Thread Pool | Microsoft Docs"
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
  - "thread pooling [.NET Framework]"
  - "thread pools [.NET Framework]"
  - "threading [.NET Framework], thread pool"
  - "threading [.NET Framework], pooling"
ms.assetid: 2be05b06-a42e-4c9d-a739-96c21d673927
caps.latest.revision: 24
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 24
---
# The Managed Thread Pool
<xref:System.Threading.ThreadPool> 类为你的应用程序提供一个受系统管理的辅助线程池，从而使你能够专注于应用程序任务，而非线程管理。  如果有需要后台处理的短任务，托管的线程池则为利用多个线程的简便方法。  例如，从 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 开始，可以创建 <xref:System.Threading.Tasks.Task> 和 <xref:System.Threading.Tasks.Task%601> 对象，它们在线程池线程上执行异步任务。  
  
> [!NOTE]
>  从 [!INCLUDE[net_v20SP1_long](../../../includes/net-v20sp1-long-md.md)] 开始，在早期版本 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 中被视为瓶颈的三个关键方面内线程池的吞吐量显著提高：队列任务、调度线程池线程和调度 I\/O 完成线程。  若要使用此功能，应用程序应为 [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)] 或更高版本。  
  
 对于与用户界面交互的后台任务，.NET Framework 2.0 版还提供 <xref:System.ComponentModel.BackgroundWorker> 类，该类使用用户界面线程上引发的事件进行通信。  
  
 .NET Framework 将线程池线程用于多种用途，包括异步 I\/O 完成、计时器回调、注册的等待操作、使用委托的异步方法调用和 <xref:System.Net> 套接字连接。  
  
## 何时不使用线程池线程  
 有几种应用场景，其中适合创建并管理自己的线程，而非使用线程池线程：  
  
-   需要一个前台线程。  
  
-   需要具有特定优先级的线程。  
  
-   拥有会导致线程长时间阻塞的任务。  线程池具有最大线程数，因此大量被阻塞的线程池线程可能会阻止任务启动。  
  
-   需将线程放入单线程单元。  所有 <xref:System.Threading.ThreadPool> 线程均位于多线程单元中。  
  
-   需具有与线程关联的稳定标识，或需将一个线程专用于一项任务。  
  
## 线程池特征  
 线程池线程是后台线程。  请参阅[Foreground and Background Threads](../../../docs/standard/threading/foreground-and-background-threads.md)。  每个线程均使用默认的堆栈大小，以默认的优先级运行，并且位于多线程单元中。  
  
 每个进程只有一个线程池。  
  
### 线程池线程中的异常  
 线程池线程上未经处理的异常终止该进程。  以下为此规则的三种例外情况：  
  
-   <xref:System.Threading.ThreadAbortException> 在线程池线程中引发，因为调用了 <xref:System.Threading.Thread.Abort%2A>。  
  
-   <xref:System.AppDomainUnloadedException> 在线程池线程中引发，因为正在卸载应用程序域。  
  
-   公共语言运行时或主机进程将终止该线程。  
  
 有关详细信息，请参阅[Exceptions in Managed Threads](../../../docs/standard/threading/exceptions-in-managed-threads.md)。  
  
> [!NOTE]
>  在 .NET framework 1.0 和 1.1 版中，公共语言运行时以无提示方式捕获线程池线程中未经处理的异常。  这可能会损坏应用程序状态并最终导致应用程序挂起，可能很难对此进行调试。  
  
### 最大线程池线程数  
 可排入线程池的操作的数量仅受可用内存限制；但是，线程池会限制可同时在进程中处于活动状态的线程数。  从 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 开始，进程的线程池的默认大小取决于若干因素，例如虚拟地址空间的大小。  进程可以调用 <xref:System.Threading.ThreadPool.GetMaxThreads%2A> 方法，以确定线程数。  
  
 可以使用 <xref:System.Threading.ThreadPool.GetMaxThreads%2A> 和 <xref:System.Threading.ThreadPool.SetMaxThreads%2A> 方法来控制最大线程数。  
  
> [!NOTE]
>  在 .NET framework 1.0 和 1.1 版中，不能在托管代码中设置线程池大小。  承载公共语言运行时的代码可使用 mscoree.h 中定义的 `CorSetMaxThreads` 来设置线程池大小。  
  
### 线程池最小值  
 线程池根据需要提供新的工作线程或 I\/O 完成线程，直到它达到每个类别的指定最小值。  可以使用 <xref:System.Threading.ThreadPool.GetMinThreads%2A> 方法来获取这些最小值。  
  
> [!NOTE]
>  需求较低时，线程池线程的实际数量可以低于最小值。  
  
 达到最小值时，线程池可以创建其他线程或等待，直到一些任务完成。  从 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 开始，线程池创建和销毁工作线程以优化吞吐量，吞吐量被定义为每个单位时间完成的任务数。  线程过少可能无法实现可用资源的最优利用，而线程过多则可能增加资源争用。  
  
> [!CAUTION]
>  可以使用 <xref:System.Threading.ThreadPool.SetMinThreads%2A> 方法来增加最小空闲线程数。  但是，不必要地增加这些值可能导致性能问题。  如果在同一时间开始太多的任务，则所有任务均可能会很慢。  大多数情况下，使用自己的分配线程算法，线程池将更好地执行任务。  
  
## 跳过安全检查  
 线程池还提供 <xref:System.Threading.ThreadPool.UnsafeQueueUserWorkItem%2A?displayProperty=fullName> 和 <xref:System.Threading.ThreadPool.UnsafeRegisterWaitForSingleObject%2A?displayProperty=fullName> 方法。  仅当确定调用方的堆栈与执行排队的任务期间进行的任何安全检查无关时，方可使用这些方法。  <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>和 <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A> 都捕获调用方的堆栈，当线程开始执行任务时，调用方的堆栈被合并到线程池线程的堆栈中。  如果安全检查是必需的，则必须检查整个堆栈。  尽管此检查提供了安全性，但它也具有性能成本。  
  
## 使用线程池  
 从 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 开始，使用线程池最简单的方法是使用[Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)。  默认情况下，并行库类型（例如 <xref:System.Threading.Tasks.Task> 和 <xref:System.Threading.Tasks.Task%601>）使用线程池线程来运行任务。  也可以通过从托管代码调用 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=fullName>（或从非托管代码调用 `CorQueueUserWorkItem`）并传递表示执行任务的方法的 <xref:System.Threading.WaitCallback> 委托来使用线程池。  使用线程池的另一种方法是通过使用 <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=fullName> 方法并传递在发出信号或超时的时候调用 <xref:System.Threading.WaitOrTimerCallback> 委托所表示的方法的 <xref:System.Threading.WaitHandle>，从而对与等待操作相关的工作项排队。  线程池线程用于调用回调方法。  
  
## 线程池示例  
 本节中的代码示例通过使用 <xref:System.Threading.Tasks.Task> 类、<xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=fullName> 方法和 <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=fullName> 方法来演示线程池。  
  
-   [使用任务并行库执行异步任务](#TaskParallelLibrary)  
  
-   [使用 QueueUserWorkItem 以异步方式执行代码](#ExecuteCodeWithQUWI)  
  
-   [为 QueueUserWorkItem 提供任务数据](#TaskDataForQUWI)  
  
-   [使用 RegisterWaitForSingleObject](#RegisterWaitForSingleObject)  
  
<a name="TaskParallelLibrary"></a>   
### 使用任务并行库执行异步任务  
 下面的示例演示如何通过调用 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=fullName> 方法来创建并使用 <xref:System.Threading.Tasks.Task> 对象。  有关使用 <xref:System.Threading.Tasks.Task%601> 类从异步任务返回值的示例，请参阅[How to: Return a Value from a Task](../../../docs/standard/parallel-programming/how-to-return-a-value-from-a-task.md)。  
  
 [!code-csharp[System.Threading.Tasks.Task#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.threading.tasks.task/cs/startnew.cs#01)]
 [!code-vb[System.Threading.Tasks.Task#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.threading.tasks.task/vb/startnew.vb#01)]  
  
<a name="ExecuteCodeWithQUWI"></a>   
### 使用 QueueUserWorkItem 以异步方式执行代码  
 下面的示例使用 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A> 方法将非常简单的任务排入队列，由 `ThreadProc` 方法表示。  
  
 [!code-cpp[Conceptual.ThreadPool#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.threadpool/cpp/source1.cpp#1)]
 [!code-csharp[Conceptual.ThreadPool#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.threadpool/cs/source1.cs#1)]
 [!code-vb[Conceptual.ThreadPool#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.threadpool/vb/source1.vb#1)]  
  
<a name="TaskDataForQUWI"></a>   
### 为 QueueUserWorkItem 提供任务数据  
 下面的代码示例使用 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A> 方法将任务排入队列，并为该任务提供数据。  
  
 [!code-cpp[Conceptual.ThreadPool#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.threadpool/cpp/source2.cpp#2)]
 [!code-csharp[Conceptual.ThreadPool#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.threadpool/cs/source2.cs#2)]
 [!code-vb[Conceptual.ThreadPool#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.threadpool/vb/source2.vb#2)]  
  
<a name="RegisterWaitForSingleObject"></a>   
### 使用 RegisterWaitForSingleObject  
 下面的示例展示多种线程处理功能。  
  
-   使用 <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A> 方法，将任务排入队列，以便由 <xref:System.Threading.ThreadPool> 线程执行。  
  
-   使用 <xref:System.Threading.AutoResetEvent> 发出要执行的任务的信号。  请参阅 [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)。  
  
-   使用 <xref:System.Threading.WaitOrTimerCallback> 委托处理超时和信号。  
  
-   使用 <xref:System.Threading.RegisteredWaitHandle> 取消排队的任务。  
  
 [!code-cpp[Conceptual.ThreadPool#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.threadpool/cpp/source3.cpp#3)]
 [!code-csharp[Conceptual.ThreadPool#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.threadpool/cs/source3.cs#3)]
 [!code-vb[Conceptual.ThreadPool#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.threadpool/vb/source3.vb#3)]  
  
## 请参阅  
 <xref:System.Threading.ThreadPool>   
 <xref:System.Threading.Tasks.Task>   
 <xref:System.Threading.Tasks.Task%601>   
 [Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)   
 [Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)   
 [How to: Return a Value from a Task](../../../docs/standard/parallel-programming/how-to-return-a-value-from-a-task.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)   
 [Threads and Threading](../../../docs/standard/threading/threads-and-threading.md)   
 [异步文件 I\/O](../../../docs/standard/io/异步文件-i-o.md)   
 [Timers](../../../docs/standard/threading/timers.md)