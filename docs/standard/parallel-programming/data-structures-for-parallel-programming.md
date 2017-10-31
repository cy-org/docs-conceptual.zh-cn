---
title: "Data Structures for Parallel Programming | Microsoft Docs"
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
  - "data structures, multi-threading"
ms.assetid: bdc82f2f-4754-45a1-a81e-fe2e9c30cef9
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Data Structures for Parallel Programming
.NET Framework 版本 4 引入了若干在并行编程中非常有用的新类型，其中包括一组并发集合类、轻量同步基元以及用于迟缓初始化的类型。  您可以将这些类型用于任何多线程应用程序代码，包括任务并行库和 PLINQ。  
  
## 并发集合类  
 <xref:System.Collections.Concurrent?displayProperty=fullName> 命名空间中的集合类提供了线程安全的添加和移除操作，这些操作能够在可能时随时避免锁，并且锁为必需时使用细粒度锁定。  与 .NET Framework 版本 1.0 和 2.0 中引入的集合不同，并发集合类不需要用户代码在访问项时采用任何锁。  在多个线程从集合中添加和移除项的情况下，并发集合类可以显著改善诸如 <xref:System.Collections.ArrayList?displayProperty=fullName> 和 <xref:System.Collections.Generic.List%601?displayProperty=fullName>（包含用户实现的锁定）等类型的性能。  
  
 下表列出了新的并发集合类：  
  
|类型|说明|  
|--------|--------|  
|<xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName>|为实现 <xref:System.Collections.Concurrent.IProducerConsumerCollection%601?displayProperty=fullName> 的线程安全集合提供阻塞和限制功能。  如果没有可用的槽或集合已满，则制造者线程将阻塞。  如果集合为空，则使用者线程将阻塞。  此类型还支持使用者和制造者的非阻塞访问。  <xref:System.Collections.Concurrent.BlockingCollection%601> 可用作基类或后备存储，为任何支持 <xref:System.Collections.Generic.IEnumerable%601> 的集合类提供阻塞和限制。|  
|<xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=fullName>|一个提供可伸缩添加和获取操作的线程安全包实现。|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName>|一个并发且可伸缩的字典类型。|  
|<xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName>|一个并发且可伸缩的 FIFO 队列。|  
|<xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=fullName>|一个并发且可伸缩的 LIFO 堆栈。|  
  
 有关详细信息，请参阅[线程安全集合](../../../docs/standard/collections/thread-safe/index.md)。  
  
## 同步基元  
 <xref:System.Threading?displayProperty=fullName> 命名空间中新的同步基元通过避免使用旧版多线程处理代码中高开销的锁定机制，实现细化的并发和更快的性能。  某些新类型（例如 <xref:System.Threading.Barrier?displayProperty=fullName> 和 <xref:System.Threading.CountdownEvent?displayProperty=fullName>）在 .NET Framework 的早期版本中没有对应项。  
  
 下表列出了这些新的同步类型：  
  
|类型|说明|  
|--------|--------|  
|<xref:System.Threading.Barrier?displayProperty=fullName>|使多个线程能够依据某种算法并行工作，方法是提供一个点，每个任务都能在该点发出其到达的信号，然后阻塞，直至部分或全部任务到达为止。  有关详细信息，请参阅[Barrier](../../../docs/standard/threading/barrier.md)。|  
|<xref:System.Threading.CountdownEvent?displayProperty=fullName>|通过提供简便的集结机制，简化了分叉和联接方案。  有关详细信息，请参阅[CountdownEvent](../../../docs/standard/threading/countdownevent.md)。|  
|<xref:System.Threading.ManualResetEventSlim?displayProperty=fullName>|一种类似于 <xref:System.Threading.ManualResetEvent?displayProperty=fullName> 的同步基元。  <xref:System.Threading.ManualResetEventSlim> 较为轻量，但只能用于进程内通信。  有关详细信息，请参阅[ManualResetEvent and ManualResetEventSlim](../../../docs/standard/threading/manualresetevent-and-manualreseteventslim.md)。|  
|<xref:System.Threading.SemaphoreSlim?displayProperty=fullName>|一种对可同时访问资源或资源池的线程数加以限制的同步基元。  有关详细信息，请参阅[Semaphore and SemaphoreSlim](../../../docs/standard/threading/semaphore-and-semaphoreslim.md)。|  
|<xref:System.Threading.SpinLock?displayProperty=fullName>|一种互斥锁基元，该基元会导致尝试获取锁的线程在生成其量程之前在循环中等待（或“旋转”）一段时间。  在等待锁的时间预期较短的情况下，<xref:System.Threading.SpinLock> 可提供比其他形式的锁定更出色的性能。  有关详细信息，请参阅[SpinLock](../../../docs/standard/threading/spinlock.md)。|  
|<xref:System.Threading.SpinWait?displayProperty=fullName>|一个小型轻量类型，该类型将旋转一段指定的时间，并在超出旋转计数的情况下最终将线程置于等待状态。有关详细信息，请参阅[SpinWait](../../../docs/standard/threading/spinwait.md)。|  
  
 有关详细信息，请参阅：  
  
-   [How to: Use SpinLock for Low\-Level Synchronization](../../../docs/standard/threading/how-to-use-spinlock-for-low-level-synchronization.md)  
  
-   [How to: Synchronize Concurrent Operations with a Barrier](../../../docs/standard/threading/how-to-synchronize-concurrent-operations-with-a-barrier.md).  
  
## 迟缓初始化类  
 对于迟缓初始化，直到在需要时才会分配对象的内存。  迟缓初始化可以在程序的生存期中平均分布对象分配，从而改善性能。  可以通过包装类型 <xref:System.Lazy%601>，为任何自定义类型启用迟缓初始化。  
  
 下表列出了迟缓初始化类型：  
  
|类型|说明|  
|--------|--------|  
|<xref:System.Lazy%601?displayProperty=fullName>|提供轻量、线程安全的迟缓初始化。|  
|<xref:System.Threading.ThreadLocal%601?displayProperty=fullName>|逐线程提供迟缓初始化的值，其中每个线程都会迟缓调用初始化函数。|  
|<xref:System.Threading.LazyInitializer?displayProperty=fullName>|提供一些静态方法，这些方法无需分配专用迟缓初始化实例，  而是使用引用来确保在访问目标时目标已初始化。|  
  
 有关详细信息，请参阅[延迟初始化](../../../docs/framework/performance/lazy-initialization.md)。  
  
## 聚合异常  
 <xref:System.AggregateException?displayProperty=fullName> 类型可用于捕获在不同线程上同时引发的多个异常，并将它们作为单个异常返回到联接线程。  <xref:System.Threading.Tasks.Task?displayProperty=fullName> 和 <xref:System.Threading.Tasks.Parallel?displayProperty=fullName> 类型以及 PLINQ 出于此目的广泛使用 <xref:System.AggregateException>。  有关更多信息，请参见[NIB: How to: Handle Exceptions Thrown by Tasks](http://msdn.microsoft.com/zh-cn/d6c47ec8-9de9-4880-beb3-ff19ae51565d)和[How to: Handle Exceptions in a PLINQ Query](../../../docs/standard/parallel-programming/how-to-handle-exceptions-in-a-plinq-query.md)。  
  
## 请参阅  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 <xref:System.Threading?displayProperty=fullName>   
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)