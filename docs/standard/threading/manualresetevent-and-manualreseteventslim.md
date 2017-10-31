---
title: "ManualResetEvent and ManualResetEventSlim | Microsoft Docs"
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
  - "threading [.NET Framework], ManualResetEvent class"
  - "ManualResetEvent class, about ManualResetEvent class"
ms.assetid: 465fdcf9-ba24-4d8d-a43f-d983b7cb0cc6
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# ManualResetEvent and ManualResetEventSlim
<xref:System.Threading.ManualResetEvent?displayProperty=fullName> 类表示一个本地等待处理事件，在该类收到信号后必须手动重置该事件。  此类表示其基类 <xref:System.Threading.EventWaitHandle?displayProperty=fullName> 的一种特殊情况。  有关手动重置事件的用法和功能，请参见 [EventWaitHandle](../../../docs/standard/threading/eventwaithandle.md) 概念文档。  
  
 在调用 <xref:System.Threading.ManualResetEvent> 对象的 <xref:System.Threading.EventWaitHandle.Reset%2A?displayProperty=fullName> 方法之前，该对象始终保持已收到信号的状态。  在对象状态为已收到信号的期间，可以释放任意多正在等待的线程，或是在事件收到信号后处理事件的线程。  <xref:System.Threading.ManualResetEvent> 对应于 Win32 `CreateEvent` 调用，它对 `bManualReset` 参数指定 `true`。  
  
 除了 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 使用此 <xref:System.Threading.ManualResetEventSlim?displayProperty=fullName> 类可以获得更好的性能，当等待时间预计非常短时以及当事件不会跨越进程边界时。  它在等待事件变为终止状态时，<xref:System.Threading.ManualResetEventSlim> 使用繁忙旋转短的时间段。  当等待时间很短时，旋转的开销相对于使用等待句柄来进行等待的开销会少很多。  但是，如果事件在某个时间段内没有变为已发出信号状态，则 <xref:System.Threading.ManualResetEventSlim> 会采用常规的事件处理等待。  
  
## 请参阅  
 [Threading](../../../docs/standard/threading/index.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)   
 [Wait Handles](../Topic/Wait%20Handles.md)   
 [AutoResetEvent](../../../docs/standard/threading/autoresetevent.md)   
 [SpinWait](../../../docs/standard/threading/spinwait.md)   
 [Semaphore and SemaphoreSlim](../../../docs/standard/threading/semaphore-and-semaphoreslim.md)