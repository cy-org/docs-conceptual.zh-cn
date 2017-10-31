---
title: "Pausing and Resuming Threads | Microsoft Docs"
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
  - "resuming threads"
  - "threading [.NET Framework], pausing"
  - "pausing threads"
ms.assetid: 9fce4859-a19d-4506-b082-7dd0792688ca
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Pausing and Resuming Threads
同步线程活动最常见的方法是阻止和释放线程，或者锁定对象或代码区域。  有关这些锁定和阻止机制的详细信息，请参阅[Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md)。  
  
 也可使线程将自身置于睡眠状态。  当线程被阻止或处于休眠状态时，可以使用 <xref:System.Threading.ThreadInterruptedException> 使它们脱离等待状态。  
  
## Thread.Sleep 方法  
 调用 <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName> 方法会导致当前线程立即被阻止，阻止时间为传递到 <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName> 的毫秒数，结果是将时间片的剩余部分生成给其他线程。  一个线程不能调用另一线程上的 <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName>。  
  
 调用 <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName> 与 <xref:System.Threading.Timeout.Infinite?displayProperty=fullName> 使线程进入睡眠状态，直到另一个调用 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> 的线程将其中断，或直到 <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> 将其终止。  
  
## 中断线程  
 可通过对被阻止的线程调用 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> 从而引发 <xref:System.Threading.ThreadInterruptedException> 来中断正在等待的线程，这将中断线程的阻止调用。  线程应该捕获 <xref:System.Threading.ThreadInterruptedException> 并执行任何适于继续工作的操作。  如果线程忽略该异常，则运行时捕获异常，并停止该线程。  
  
> [!NOTE]
>  如果在调用 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> 时，未阻止目标线程，则线程在被阻止前将不会中断。  如果线程永远不被阻止，则它可在不被中断的情况下完成。  
  
 如果等待是托管的等待，则 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> 和 <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> 都会立即唤醒线程。  如果等待是非托管的等待（例如，调用 Win32 `WaitForSingleObject` 函数的平台调用），则 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> 和 <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> 都不能控制线程，直到它返回到或调入托管代码。  在托管代码中，该行为如下：  
  
-   <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> 将线程从其可能处于的任何等待中唤醒，并导致在目标线程中引发 <xref:System.Threading.ThreadInterruptedException>。  
  
-   <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> 类似于 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName>，其区别在于它会导致在线程上引发 <xref:System.Threading.ThreadAbortException>。  有关详细信息，请参阅[销毁线程](../../../docs/standard/threading/destroying-threads.md)。  
  
## 挂起和继续（已过时）  
 <xref:System.Threading.Thread> 类包括两个方法，<xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> 和 <xref:System.Threading.Thread.Resume%2A?displayProperty=fullName>，用于暂停和继续一个线程。  但是，不建议使用这些方法。  
  
> [!IMPORTANT]
>  从 .NET Framework 2.0 版开始，将 <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> 和 <xref:System.Threading.Thread.Resume%2A?displayProperty=fullName> 方法标记为已过时，并将在未来的版本中删除。  
>   
>  <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> 和 <xref:System.Threading.Thread.Resume%2A?displayProperty=fullName> 方法通常不适用于应用程序，并且不应将其与同步机制混淆。  因为 <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> 和 <xref:System.Threading.Thread.Resume%2A?displayProperty=fullName> 不依赖于受控线程的协作，所以它们极具侵犯性并且可导致严重的应用程序问题，如死锁（例如，如果你挂起一个占用另一个线程所需资源的线程）。  
  
 某些应用程序需要控制线程的优先级，以便获得更好的性能。  若要执行此操作，应使用 <xref:System.Threading.Thread.Priority%2A?displayProperty=fullName> 属性，而非 <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName>。  
  
## 请参阅  
 <xref:System.Threading.Thread>   
 <xref:System.Threading.ThreadInterruptedException>   
 <xref:System.Threading.ThreadAbortException>   
 [Threading](../../../docs/standard/threading/index.md)   
 [Using Threads and Threading](../../../docs/standard/threading/using-threads-and-threading.md)   
 [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md)