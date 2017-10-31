---
title: "How to: Use SpinLock for Low-Level Synchronization | Microsoft Docs"
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
  - "SpinLock, how to use"
ms.assetid: a9ed3e4e-4f29-4207-b730-ed0a51ecbc19
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# How to: Use SpinLock for Low-Level Synchronization
下面的示例演示如何使用 <xref:System.Threading.SpinLock>。  
  
## 示例  
 在本示例中，关键部分执行最少量的工作，因而是一个不错的 <xref:System.Threading.SpinLock> 备选。  相比较于标准锁来说，增加一点工作量即可提高 <xref:System.Threading.SpinLock> 的性能。  但需注意的一点是，SpinLock 比标准锁更耗费资源。  您可以使用分析工具中并发分析功能，查看哪种类型的锁可以在您的程序中提供更好的性能。  有关更多信息，请参见[并发可视化工具](../Topic/Concurrency%20Visualizer.md)。  
  
 [!code-csharp[CDS_SpinLock#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinlock/cs/spinlockdemo.cs#02)]
 [!code-vb[CDS_SpinLock#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinlock/vb/spinlock_vb.vb#02)]  
  
 <xref:System.Threading.SpinLock> 对于很长时间都不会持有共享资源上的锁的情况可能很有用。  对于此类情况，在多核计算机上，一种有效的做法是让已阻塞的线程旋转几个周期，直至锁被释放。  通过旋转，线程将不会进入阻塞状态（这是一个占用大量 CPU 资源的过程）。  在某些情况下，<xref:System.Threading.SpinLock> 将会停止旋转，以防止出现逻辑处理器资源不足的现象，或出现系统上超线程的优先级反转的情况。  
  
 此示例使用 <xref:System.Collections.Generic.Queue%601?displayProperty=fullName> 类，这要求针对多线程的访问进行用户同步。  在以 .NET Framework 4 为目标的应用程序中，还可以选择使用 <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName>，这不需要任何用户锁。  
  
 请注意，在对 <xref:System.Threading.SpinLock.Exit%2A> 的调用中使用了 `false`（在 Visual Basic 中为 `False`）。  这样可以提供最佳性能。  在 IA64 架构上指定 `true` \(`True`\) 可使用内存界定，它会刷新写入缓冲区以确保锁现在可供其他线程用来退出。  
  
## 请参阅  
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)