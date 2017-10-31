---
title: "Overview of Synchronization Primitives | Microsoft Docs"
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
  - "synchronization, threads"
  - "threading [.NET Framework],synchronizing threads"
  - "managed threading"
ms.assetid: b782bcb8-da6a-4c6a-805f-2eb46d504309
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Overview of Synchronization Primitives
.NET Framework 提供了一系列用于控制线程交互和避免争用情况的同步基元。  这大致可分为 3 个类别：锁定、发出信号和联锁操作。  
  
 类别不整齐也非明确定义：某些同步机制具有多个类别的特征；一次释放一个线程的事件在功能上类似锁定；任何锁定的释放可均可被视为一个信号；并且联锁操作可用于构造锁定。  但是，类别仍然有用。  
  
 请务必记住线程同步是协作的。  即使是某个线程绕过同步机制直接访问了受保护的资源，此同步机制也不能为有效机制。  
  
 本概述包含以下几节：  
  
-   [锁定](#locking)  
  
-   [Signaling](#signaling)  
  
-   [轻量同步类型](#lightweight_synchronization_types)  
  
-   [SpinWait](#spinwait)  
  
-   [互锁操作](#interlocked_operations)  
  
<a name="locking"></a>   
## 锁定  
 锁定控制一次针对一个线程的资源，或控制针对指定数目线程的资源。  锁定正在使用时请求排他锁的线程将受阻，直到锁定变为可用。  
  
### 排他锁  
 锁定的最简单形式是 C\# `lock` 语句（Visual Basic 中为 `SyncLock`），它控制对代码块的访问。  此类块经常被称为关键部分。  `lock` 语句通过使用 <xref:System.Threading.Monitor> 类的 <xref:System.Threading.Monitor.Enter%2A> 和 <xref:System.Threading.Monitor.Exit%2A> 方法实现，并且使用 `try…catch…finally` 确保锁定已释放。  
  
 通常，使用 <xref:System.Threading.Monitor> 类的最佳方式是使用 `lock` 语句来保护小的代码块，决不使用超过一个简单方法。  <xref:System.Threading.Monitor> 类虽然功能强大，但容易形成孤立锁和死锁情况。  
  
#### Monitor 类  
 <xref:System.Threading.Monitor> 类提供了附加功能，可以与 `lock` 语句配合使用：  
  
-   <xref:System.Threading.Monitor.TryEnter%2A> 方法允许受阻线程等待资源在指定的时间间隔后放弃。  它返回一个指示成功或失败布尔值，该值可用于检测和避免潜在的死锁。  
  
-   <xref:System.Threading.Monitor.Wait%2A> 方法由关键部分中的线程调用。  它放弃对资源和块的控制，直到资源再次可用。  
  
-   <xref:System.Threading.Monitor.Pulse%2A> 和 <xref:System.Threading.Monitor.PulseAll%2A> 方法允许将要释放锁或要调用 <xref:System.Threading.Monitor.Wait%2A> 的线程将一个或多个线程放置到准备就绪的队列中，以便它们能够获取此锁。  
  
 <xref:System.Threading.Monitor.Wait%2A>方法重载上的超时允许正在等待的线程跳转到就绪的队列。  
  
 如果用于锁的对象派生自<xref:System.MarshalByRefObject>，则 <xref:System.Threading.Monitor> 类可以在多个应用程序域中提供锁定。  
  
 <xref:System.Threading.Monitor> 具有线程关联。  即，进入监视器的线程必须通过调用 <xref:System.Threading.Monitor.Exit%2A> 或 <xref:System.Threading.Monitor.Wait%2A> 退出。  
  
 <xref:System.Threading.Monitor> 类不可实例化。  其方法是静态方法（Visual Basic 中为 `Shared`），并在用于可实例化的锁对象。  
  
 有关概念性概述，请参阅[监视器](../Topic/Monitors.md)。  
  
#### Mutex 类  
 线程通过调用其 <xref:System.Threading.WaitHandle.WaitOne%2A> 方法的重载来请求 <xref:System.Threading.Mutex>。  提供了超时的重载，以允许线程放弃等待。  与 <xref:System.Threading.Monitor> 类不同，互斥可以是局部的，也可以是全局的。  全局互斥（也称为已命名互斥）在整个操作系统中均可见，且可用于同步多个应用程序域或进程中的线程。  局部互斥派生自 <xref:System.MarshalByRefObject>，且可跨应用程序域边界使用。  
  
 此外，<xref:System.Threading.Mutex> 派生自 <xref:System.Threading.WaitHandle>，这意味着它可以与 <xref:System.Threading.WaitHandle> 提供的信号机制（如 <xref:System.Threading.WaitHandle.WaitAll%2A>、<xref:System.Threading.WaitHandle.WaitAny%2A> 和 <xref:System.Threading.WaitHandle.SignalAndWait%2A> 方法）一起使用。  
  
 和 <xref:System.Threading.Monitor> 一样，<xref:System.Threading.Mutex> 也具有线程关联。  与 <xref:System.Threading.Monitor> 不同，<xref:System.Threading.Mutex> 是可实例化的对象。  
  
 有关概念性概述，请参阅[Mutexes](../../../docs/standard/threading/mutexes.md)。  
  
#### SpinLock 类  
 从 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 起，当 <xref:System.Threading.Monitor> 要求的开销降低了性能时，可以使用 <xref:System.Threading.SpinLock> 类。  当 <xref:System.Threading.SpinLock> 遇到锁定关键部分时，它只在循环中旋转，直到锁变为可用。  如果锁被保留的时间很短，旋转可以比阻止提供更好的性能。  但是，如果锁被保留超过数十个周期数，<xref:System.Threading.SpinLock> 与<xref:System.Threading.Monitor> 的性能相同，但将使用更多 CPU 周期，因此会降低其他线程或进程的性能。  
  
### 其他锁  
 锁不必为排他锁。  在允许有限数量的线程并发访问资源时，这通常很有用。  信号量和读取器\/编写器锁旨在控制此类连入池的资源访问。  
  
#### ReaderWriterLock 类  
 <xref:System.Threading.ReaderWriterLockSlim> 类解决了更改数据的线程（即编写器）必须具有资源的独占访问权的情况。  编写器处于非活动状态时，任意数量的读取器均可访问资源（例如，通过调用 <xref:System.Threading.ReaderWriterLockSlim.EnterReadLock%2A> 方法）。  当某个线程请求独占访问时，（例如，通过调用 <xref:System.Threading.ReaderWriterLockSlim.EnterWriteLock%2A> 方法），后续读取器请求将被阻止，直到所有现有读取器均已退出锁，并且编写器已进入并退出锁。  
  
 <xref:System.Threading.ReaderWriterLockSlim> 具有线程关联。  
  
 有关概念性概述，请参阅[Reader\-Writer Locks](../../../docs/standard/threading/reader-writer-locks.md)。  
  
#### Semaphore 类  
 <xref:System.Threading.Semaphore> 类允许指定数量的线程访问资源。  请求资源的其他线程将受阻，直到一个线程释放信号量。  
  
 和 <xref:System.Threading.Mutex> 类一样，<xref:System.Threading.Semaphore> 也派生自 <xref:System.Threading.WaitHandle>。  也和 <xref:System.Threading.Mutex>一样，<xref:System.Threading.Semaphore> 可以是局部的，也可以是全局的。  它也可跨应用程序域边界使用。  
  
 与 <xref:System.Threading.Monitor>、<xref:System.Threading.Mutex> 和<xref:System.Threading.ReaderWriterLock> 不同，<xref:System.Threading.Semaphore> 不具有线程关联。  这意味着它可以在一个线程获取信号量而另一个线程释放此信号量的情况下使用。  
  
 有关概念性概述，请参阅[Semaphore and SemaphoreSlim](../../../docs/standard/threading/semaphore-and-semaphoreslim.md)。  
  
 <xref:System.Threading.SemaphoreSlim?displayProperty=fullName> 是单个流程边界内用于同步的轻量级信号量。  
  
 [返回页首](#top)  
  
<a name="signaling"></a>   
## Signaling  
 等待来自另一个线程的信号的最简单方法是调用 <xref:System.Threading.Thread.Join%2A> 方法，此方法在其他线程完成前受阻。  <xref:System.Threading.Thread.Join%2A> 具有两个重载，允许受阻线程在经过指定的时间间隔后跳出等待。  
  
 等待句柄提供一组更为丰富的等待和信号功能。  
  
### 等待句柄  
 等待句柄派生自 <xref:System.Threading.WaitHandle> 类，后者转而派生自 <xref:System.MarshalByRefObject>。  因此，等待句柄可用于跨应用程序域边界同步线程的活动。  
  
 线程通过调用实例方法 <xref:System.Threading.WaitHandle.WaitOne%2A> 或其中一个静态方法（<xref:System.Threading.WaitHandle.WaitAll%2A>、<xref:System.Threading.WaitHandle.WaitAny%2A> 或 <xref:System.Threading.WaitHandle.SignalAndWait%2A>来阻止等待句柄。  释放方式取决于调用的方法类型和等待句柄的类型。  
  
 有关概念性概述，请参阅 [Wait Handles](../Topic/Wait%20Handles.md)。  
  
#### 事件等待句柄  
 事件等待句柄包括 <xref:System.Threading.EventWaitHandle>类及其派生类（<xref:System.Threading.AutoResetEvent> 和 <xref:System.Threading.ManualResetEvent>）。  当通过调用事件等待句柄的 <xref:System.Threading.EventWaitHandle.Set%2A> 方法或通过使用 <xref:System.Threading.WaitHandle.SignalAndWait%2A> 方法来发出事件等待句柄的信号时，将从事件等待句柄中释放线程。  
  
 事件等待句柄可以像旋转栅在每次发出信号时仅允许一个线程通过一样，自动对进行重置，也可以像接收到信号前保持关闭、然后在被关闭前保持打开的大门一样，必须手动进行重置。  顾名思义，<xref:System.Threading.AutoResetEvent> 和 <xref:System.Threading.ManualResetEvent> 分别表示前者和后者。  <xref:System.Threading.ManualResetEventSlim?displayProperty=fullName> 是单个流程边界内用于同步的轻量事件。  
  
 <xref:System.Threading.EventWaitHandle> 可表示其中任一类型的事件，并且可为局部也可为全局。  派生类 <xref:System.Threading.AutoResetEvent> 和 <xref:System.Threading.ManualResetEvent> 始终是局部的。  
  
 事件等待句柄不具有线程关联。  任何线程均可以向事件等待句柄发送信号。  
  
 有关概念性概述，请参阅 [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)。  
  
#### Mutex 和 Semaphore 类  
 因为 <xref:System.Threading.Mutex> <xref:System.Threading.Semaphore> 类派生自 <xref:System.Threading.WaitHandle>，因此可与 <xref:System.Threading.WaitHandle> 的静态方法一起使用。  例如，线程可以使用 <xref:System.Threading.WaitHandle.WaitAll%2A> 方法来等待直到以下全部 3 个条件均为 True：向<xref:System.Threading.EventWaitHandle> 发出信号，释放了 <xref:System.Threading.Mutex>，且释放了 <xref:System.Threading.Semaphore>。  同样，线程可使用<xref:System.Threading.WaitHandle.WaitAny%2A> 方法等待直到其中任一条件为 true。  
  
 对于 <xref:System.Threading.Mutex> 或 <xref:System.Threading.Semaphore>，被发送信号意味着被释放。  如果两者中任一类型被用作 <xref:System.Threading.WaitHandle.SignalAndWait%2A> 方法的第一个参数，则将其释放。  对于具有线程关联的 <xref:System.Threading.Mutex>，如果调用线程不具有互斥，则引发异常。  按前面所述，信号量不具有线程关联。  
  
#### 屏障  
 <xref:System.Threading.Barrier> 类提供了一种以循环方式同步多个线程的方法，以便所有线程在同一个点受阻并等待其他线程完成。  一个或多个线程需要另一个线程的结果时，继续到算法的下一阶段之前，一个屏障很有用。  有关详细信息，请参阅[Barrier](../../../docs/standard/threading/barrier.md)。  
  
 [返回页首](#top)  
  
<a name="lightweight_synchronization_types"></a>   
## 轻量同步类型  
 从 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]起，可在可能时使用同步基元，该基元通过避免 Win32 内核对象（如等待句柄）上造成高开销的依赖提供快速性能。  通常，在当等待时间较短且仅当已尝试并发现原始同步类型让人不满意时，才应使用这些类型。  在需要跨进程通信的情况下，不能使用轻量类型。  
  
-   <xref:System.Threading.SemaphoreSlim?displayProperty=fullName> 是 <xref:System.Threading.Semaphore?displayProperty=fullName> 的轻量版本。  
  
-   <xref:System.Threading.ManualResetEventSlim?displayProperty=fullName> 是 <xref:System.Threading.ManualResetEvent?displayProperty=fullName> 的轻量版本。  
  
-   <xref:System.Threading.CountdownEvent?displayProperty=fullName> 表示当其计数为零时将被发送信号的事件。  
  
-   <xref:System.Threading.Barrier?displayProperty=fullName> 使多个线程能够相互同步而无需由主线程控制。  屏障会阻止每个线程继续，直到所有线程均已到达指定点。  
  
 [返回页首](#top)  
  
<a name="spinwait"></a>   
## SpinWait  
 从 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]起，当线程必须等待事件接收信号或必须满足某种条件时，可以使用 <xref:System.Threading.SpinWait?displayProperty=fullName> 结构，但如果实际等待时间预计小于使用等待句柄或阻止当前线程所需的等待时间时，则不能使用。  通过使用 <xref:System.Threading.SpinWait>，你可以指定等待期间要旋转的一小段时间，且只在特定时间不满足条件时让行（例如，通过等待或休眠）。  
  
 [返回页首](#top)  
  
<a name="interlocked_operations"></a>   
## 互锁操作  
 联锁操作是 <xref:System.Threading.Interlocked> 类的静态方法在内存位置执行的简单原子操作。  这些原子操作包括添加、递增和递减、交换、取决于比较的条件交换以及在 32 位平台上读取 64 位值的操作。  
  
> [!NOTE]
>  仅保证单个操作的原子性；当多个操作必须作为一个单元执行时，必须使用更粗粒度的同步机制。  
  
 尽管这些操作均不是锁或信号，但可用于构造锁和信号。  它们源于 Windows 操作系统，因此联锁操作非常快。  
  
 联锁操作可以与易失内存保证一起使用，用于编写展示强大的非阻塞并发功能的应用程序。  但是，它们需要复杂的、低级别编程，因此在大多数情况下，简单锁是更好的选择。  
  
 有关概念性概述，请参阅[Interlocked Operations](../../../docs/standard/threading/interlocked-operations.md)。  
  
## 请参阅  
 [Synchronizing Data for Multithreading](../../../docs/standard/threading/synchronizing-data-for-multithreading.md)   
 [监视器](../Topic/Monitors.md)   
 [Mutexes](../../../docs/standard/threading/mutexes.md)   
 [Semaphore and SemaphoreSlim](../../../docs/standard/threading/semaphore-and-semaphoreslim.md)   
 [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)   
 [Wait Handles](../Topic/Wait%20Handles.md)   
 [Interlocked Operations](../../../docs/standard/threading/interlocked-operations.md)   
 [Reader\-Writer Locks](../../../docs/standard/threading/reader-writer-locks.md)   
 [Barrier](../../../docs/standard/threading/barrier.md)   
 [SpinWait](../../../docs/standard/threading/spinwait.md)   
 [SpinLock](../../../docs/standard/threading/spinlock.md)