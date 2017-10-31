---
title: "托管线程状态 | Microsoft Docs"
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
  - "线程处理 [.NET Framework], 状态"
ms.assetid: 63890d5e-6025-4a7c-aaf0-d8bfd54b455f
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 托管线程状态
<xref:System.Threading.Thread.ThreadState%2A?displayProperty=fullName> 属性提供了一个位掩码，用以指示线程的当前状态。 一个线程始终处于 <xref:System.Threading.ThreadState> 枚举中的至少一个可能状态，并且可以同时处于多个状态。  
  
> [!IMPORTANT]
>  线程状态仅涉及几个调试方案。 因此，始终不应在代码中使用线程状态来同步线程活动。  
  
 创建托管线程时，该线程处于 <xref:System.Threading.ThreadState> 状态。 线程会一直保持 <xref:System.Threading.ThreadState> 状态，直到操作系统将其转移到已启动状态。 调用 <xref:System.Threading.Thread.Start%2A> 使操作系统知道该线程可启动；它不会更改线程的状态。  
  
 进入托管环境的非托管线程已处于已启动状态。 线程处于已启动状态后，可以执行许多操作来使线程更改状态。 下表列出了使状态发生更改的操作和相应的新状态  
  
|操作|所得到的新状态|  
|--------|-------------|  
|调用 <xref:System.Threading.Thread> 类的构造函数。|<xref:System.Threading.ThreadState>|  
|另一个线程调用 <xref:System.Threading.Thread.Start%2A?displayProperty=fullName>。|<xref:System.Threading.ThreadState>|  
|线程响应 <xref:System.Threading.Thread.Start%2A?displayProperty=fullName> 并开始运行。|<xref:System.Threading.ThreadState>|  
|线程调用 <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName>。|<xref:System.Threading.ThreadState>|  
|线程在另一个对象上调用 <xref:System.Threading.Monitor.Wait%2A?displayProperty=fullName>。|<xref:System.Threading.ThreadState>|  
|线程在另一个线程上调用 <xref:System.Threading.Thread.Join%2A?displayProperty=fullName>。|<xref:System.Threading.ThreadState>|  
|另一个线程调用 <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName>。|<xref:System.Threading.ThreadState>|  
|线程响应 <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> 请求。|<xref:System.Threading.ThreadState>|  
|另一个线程调用 <xref:System.Threading.Thread.Resume%2A?displayProperty=fullName>。|<xref:System.Threading.ThreadState>|  
|另一个线程调用 <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName>。|<xref:System.Threading.ThreadState>|  
|线程响应 <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName>。|<xref:System.Threading.ThreadState>，然后 <xref:System.Threading.ThreadState>|  
  
 由于 <xref:System.Threading.ThreadState> 状态具有值 0，因此它不能执行位测试来发现此状态。 相反，可以使用以下测试（以伪代码表示）：  
  
```  
if ((state & (Unstarted | Stopped)) == 0)   // implies Running     
```  
  
 在任何给定时间，线程通常处于多个状态。 例如，如果某个线程在 <xref:System.Threading.Monitor.Wait%2A?displayProperty=fullName> 调用上被阻止并且另一个线程在该线程上调用 <xref:System.Threading.Thread.Abort%2A>，则该线程将同时处于 <xref:System.Threading.ThreadState> 和 <xref:System.Threading.ThreadState> 状态。 在这种情况下，一旦该线程从对<xref:System.Threading.Monitor.Wait%2A> 的调用返回或该线程中断，它就会收到 <xref:System.Threading.ThreadAbortException>。  
  
 线程由于调用 <xref:System.Threading.Thread.Start%2A> 而离开 <xref:System.Threading.ThreadState> 状态后，它将无法再返回到 <xref:System.Threading.ThreadState> 状态。 同样，线程也永远无法离开 <xref:System.Threading.ThreadState> 状态。  
  
## 请参阅  
 <xref:System.Threading.ThreadAbortException>   
 <xref:System.Threading.Thread>   
 <xref:System.Threading.ThreadState>   
 [Threading](../../../docs/standard/threading/index.md)