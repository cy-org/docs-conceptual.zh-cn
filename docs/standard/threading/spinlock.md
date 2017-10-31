---
title: "SpinLock | Microsoft Docs"
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
  - "synchronization primitives, SpinLock"
ms.assetid: f9af93bb-7a0d-4ba5-afe8-74f48b6b6958
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# SpinLock
<xref:System.Threading.SpinLock> 结构是一个低级别的互斥同步基元，它在等待获取锁时进行旋转。  在多核计算机上，当等待时间预计较短且极少出现争用情况时，<xref:System.Threading.SpinLock> 的性能将高于其他类型的锁。  不过，我们建议您仅在通过分析确定 <xref:System.Threading.Monitor?displayProperty=fullName> 方法或 <xref:System.Threading.Interlocked> 方法显著降低了程序的性能时使用 <xref:System.Threading.SpinLock>。  
  
 即使 <xref:System.Threading.SpinLock> 未获取锁，它也会产生线程的时间片。  它这样做是为了避免线程优先级别反转，并使垃圾回收器能够继续执行。  在使用 <xref:System.Threading.SpinLock> 时，请确保任何线程持有锁的时间不会超过一个非常短的时间段，并确保任何线程在持有锁时不会阻塞。  
  
 由于 SpinLock 是一个值类型，因此，如果您希望两个副本都引用同一个锁，则必须通过引用显式传递该锁。  
  
 有关如何使用此类型的更多信息，请参见 <xref:System.Threading.SpinLock?displayProperty=fullName>。  有关示例，请参见[How to: Use SpinLock for Low\-Level Synchronization](../../../docs/standard/threading/how-to-use-spinlock-for-low-level-synchronization.md)。  
  
 <xref:System.Threading.SpinLock> 支持线程跟踪模式，可以在开发阶段使用此模式来帮助跟踪在特定时间持有锁的线程。  虽然线程跟踪模式对于调试很有用，但我们建议您在程序的发行版本中将其禁用，因为此模式可能会导致性能降低。  有关更多信息，请参见[How to: Enable Thread\-Tracking Mode in SpinLock](../../../docs/standard/threading/how-to-enable-thread-tracking-mode-in-spinlock.md)。  
  
## 请参阅  
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)