---
title: "EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent | Microsoft Docs"
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
  - "wait handles"
  - "threading [.NET Framework], EventWaitHandle class"
  - "event wait handles [.NET Framework]"
ms.assetid: cd94fc34-ac15-427f-b723-a1240a4fab7d
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent
事件等待句柄允许线程通过彼此发送信号和等待彼此的信号来同步活动。  这些同步事件是基于 Win32 等待句柄的，可分为两种类型：一种收到信号时自动重置；另一种需手动重置。  
  
 事件等待句柄在与 <xref:System.Threading.Monitor> 类相同的许多同步情况下十分有用。  事件等待句柄通常比使用 <xref:System.Threading.Monitor.Wait%2A?displayProperty=fullName> 和 <xref:System.Threading.Monitor.Pulse%2A?displayProperty=fullName> 方法更简单，并且可以对信号发送提供更多控制。  命名事件等待句柄也可用于跨应用程序域和进程同步活动，而监视器对于应用程序域是本地的。  
  
## 本节内容  
 [EventWaitHandle](../../../docs/standard/threading/eventwaithandle.md)  
 <xref:System.Threading.EventWaitHandle> 类可以表示自动或手动重置事件以及本地事件或命名系统事件。  
  
 [AutoResetEvent](../../../docs/standard/threading/autoresetevent.md)  
 <xref:System.Threading.AutoResetEvent> 类派生自 <xref:System.Threading.EventWaitHandle>，表示自动重置的本地事件。  
  
 [ManualResetEvent and ManualResetEventSlim](../../../docs/standard/threading/manualresetevent-and-manualreseteventslim.md)  
 <xref:System.Threading.ManualResetEvent> 类派生自 <xref:System.Threading.EventWaitHandle>，表示必须手动重置的本地事件。  <xref:System.Threading.ManualResetEventSlim> 类是可用于同一进程中的事件的轻型快速版本。  
  
 [CountdownEvent](../../../docs/standard/threading/countdownevent.md)  
 <xref:System.Threading.CountdownEvent> 类提供一种在使用等待句柄的代码中实现分离\/连接并行模式的简单方法。  
  
## 相关章节  
 [Wait Handles](../Topic/Wait%20Handles.md)  
 <xref:System.Threading.WaitHandle> 类是 <xref:System.Threading.EventWaitHandle>、<xref:System.Threading.Semaphore> 和 <xref:System.Threading.Mutex> 类的基类。  它包含在处理所有类型的等待句柄时十分有用的静态方法，如 <xref:System.Threading.WaitHandle.SignalAndWait%2A> 和 <xref:System.Threading.WaitHandle.WaitAll%2A>。  
  
## 请参阅  
 <xref:System.Threading.EventWaitHandle>   
 <xref:System.Threading.WaitHandle>   
 <xref:System.Threading.AutoResetEvent>   
 <xref:System.Threading.ManualResetEvent>   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)   
 [Managed Threading Basics](../../../docs/standard/threading/managed-threading-basics.md)