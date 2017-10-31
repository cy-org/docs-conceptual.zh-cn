---
title: "CountdownEvent | Microsoft Docs"
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
  - "synchronization primitives, CountdownEvent"
ms.assetid: eec3812a-e20f-4ecd-bfef-6921d508b708
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# CountdownEvent
<xref:System.Threading.CountdownEvent?displayProperty=fullName> 是一个同步基元，它在收到一定次数的信号之后，将会解除对其等待线程的锁定。  <xref:System.Threading.CountdownEvent> 专门用于以下情况：您必须使用 <xref:System.Threading.ManualResetEvent> 或 <xref:System.Threading.ManualResetEventSlim>，并且必须在用信号通知事件之前手动递减一个变量。  例如，在分叉\/联接方案中，您可以只创建一个信号计数为 5 的 <xref:System.Threading.CountdownEvent>，然后在线程池上启动五个工作项，并且让每个工作项在完成时调用 <xref:System.Threading.CountdownEvent.Signal%2A>。  每次调用 <xref:System.Threading.CountdownEvent.Signal%2A> 时，信号计数都会递减 1。  在主线程上，对 <xref:System.Threading.CountdownEvent.Wait%2A> 的调用将会阻塞，直至信号计数为零。  
  
> [!NOTE]
>  对于不必与旧版 .NET Framework 同步 API 进行交互的代码，可考虑使用 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 对象或 <xref:System.Threading.Tasks.Parallel.Invoke%2A> 方法来获取一种更简单的表示分叉\-联接并行度的方式。  
  
 <xref:System.Threading.CountdownEvent> 具有这些附加功能：  
  
-   可通过使用取消标记来取消等待操作。  
  
-   创建实例之后可以递增它的信号计数。  
  
-   通过调用 <xref:System.Threading.CountdownEvent.Reset%2A> 方法，可在 <xref:System.Threading.CountdownEvent.Wait%2A> 返回之后重用实例。  
  
-   实例公开 <xref:System.Threading.WaitHandle> 以便与其他 .NET Framework 同步 API（例如 <xref:System.Threading.WaitHandle.WaitAll%2A>）进行集成。  
  
## 基本用法  
 下面的示例演示如何与 <xref:System.Threading.ThreadPool> 工作项一起使用 <xref:System.Threading.CountdownEvent>。  
  
 [!code-csharp[CDS_CountdownEvent#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#01)]
 [!code-vb[CDS_CountdownEvent#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/module1.vb#01)]  
  
## 使用取消标记的 CountdownEvent  
 下面的示例演示如何通过使用取消标记来取消对于 <xref:System.Threading.CountdownEvent> 的等待操作。  基本模式遵循在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]中引入的统一取消的模型。  有关更多信息，请参见[Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)。  
  
 [!code-csharp[CDS_CountdownEvent#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#02)]
 [!code-vb[CDS_CountdownEvent#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/canceleventwait.vb#02)]  
  
 请注意，等待操作不会取消正在向其发出信号的线程。  通常，将取消应用于逻辑操作，这类逻辑操作可以包括等待事件以及等待操作正在同步的所有工作项。  在本示例中，将为每个工作项传递同一个取消标记，以便它们可以响应取消请求。  
  
## 请参阅  
 [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)