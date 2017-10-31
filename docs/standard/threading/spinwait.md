---
title: "SpinWait | Microsoft Docs"
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
  - "synchronization primitives, SpinWait"
ms.assetid: 36012f42-34e5-4f86-adf4-973f433ed6c6
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# SpinWait
<xref:System.Threading.SpinWait?displayProperty=fullName> 是一个轻量同步类型，可以在低级别方案中使用它来避免内核事件所需的高开销的上下文切换和内核转换。  在多核计算机上，当预计资源不会保留很长一段时间时，如果让等待线程以用户模式旋转数十或数百个周期，然后重新尝试获取资源，则效率会更高。  如果在旋转后资源变为可用的，则可以节省数千个周期。  如果资源仍然不可用，则只花费了少量周期，并且仍然可以进行基于内核的等待。  这一旋转\-等待的组合有时称为“两阶段等待操作”。  
  
 <xref:System.Threading.SpinWait> 旨在与包装内核事件（例如 <xref:System.Threading.ManualResetEvent>）的 .NET Framework 类型配合使用。  <xref:System.Threading.SpinWait> 还可以自行用于仅限在一个程序中使用的基本旋转功能。  
  
 <xref:System.Threading.SpinWait> 不仅仅是一个空循环。  它经过了精心实现，可以针对一般情况提供正确的旋转行为，而且还可以在旋转时间足够长（大致为内核转换所需的时间长度）的情况下自行启动上下文切换。  例如，在单核计算机上，<xref:System.Threading.SpinWait> 会立即产生线程的时间片，因为旋转将阻塞所有线程向前进展。  <xref:System.Threading.SpinWait> 甚至还会在多核计算机上产生线程的时间片以防止等待线程阻塞高优先级的线程或垃圾回收器。  因此，如果您在两阶段等待操作中使用 <xref:System.Threading.SpinWait>，则建议您在 <xref:System.Threading.SpinWait> 自行启动上下文切换之前调用内核等待。  <xref:System.Threading.SpinWait> 提供 <xref:System.Threading.SpinWait.NextSpinWillYield%2A> 属性，您可在每次调用 <xref:System.Threading.SpinWait.SpinOnce%2A> 之前检查该属性。  当该属性返回 `true` 时，将启动您自己的等待操作。  有关示例，请参见[How to: Use SpinWait to Implement a Two\-Phase Wait Operation](../../../docs/standard/threading/how-to-use-spinwait-to-implement-a-two-phase-wait-operation.md)。  
  
 如果您不是在执行两阶段等待操作，而只是旋转等待某个条件为 true，则可使 <xref:System.Threading.SpinWait> 执行它的上下文切换，以便它在 Windows 操作系统环境中是一个好公民。  下面的基本示例演示了无锁堆栈中的 <xref:System.Threading.SpinWait>。  如果您需要高性能的线程安全的堆栈，请考虑使用 <xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=fullName>。  
  
 [!code-csharp[CDS_SpinWait#05](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinwait/cs/spinwait.cs#05)]
 [!code-vb[CDS_SpinWait#05](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinwait/vb/cds_spinwait1.vb#05)]  
  
## 请参阅  
 <xref:System.Threading.Thread.SpinWait%2A>   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)