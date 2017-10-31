---
title: "Reader-Writer Locks | Microsoft Docs"
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
  - "ReaderWriterLock class, about ReaderWriterLock class"
  - "threading [.NET Framework], ReaderWriterLock class"
ms.assetid: 8c71acf2-2c18-4f4d-8cdb-0728639265fd
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Reader-Writer Locks
<xref:System.Threading.ReaderWriterLockSlim> 类允许多个线程同时读取一个资源，但在向该资源写入时要求线程等待以获得独占锁。  
  
 可以在应用程序中使用 <xref:System.Threading.ReaderWriterLockSlim>，以便在访问一个共享资源的线程之间提供协调同步。  获得的锁是针对 <xref:System.Threading.ReaderWriterLockSlim> 本身的。  
  
 与任何线程同步机制相同，您必须确保任何线程都不会跳过 <xref:System.Threading.ReaderWriterLockSlim> 提供的锁定。  确保做到这一点的一种方法是设计一个封装该共享资源的类。  此类将提供访问专用共享资源以及使用专用 <xref:System.Threading.ReaderWriterLockSlim> 进行同步的成员。  有关示例，请参见 <xref:System.Threading.ReaderWriterLockSlim> 类的代码示例。  <xref:System.Threading.ReaderWriterLockSlim> 的效率足以用于同步各个对象。  
  
 设计您应用程序的结构，让读取和写入操作的时间尽可能最短。  因为写入锁是排他的，所以长时间的写入操作会直接影响吞吐量。  长时间的读取操作会阻止处于等待状态的编写器，并且，如果至少有一个线程在等待写入访问，则请求读取访问的线程也将被阻止。  
  
> [!NOTE]
>  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 具有两个读取器\/编写器锁：<xref:System.Threading.ReaderWriterLockSlim> 和 <xref:System.Threading.ReaderWriterLock>。  对于所有新的开发建议使用 <xref:System.Threading.ReaderWriterLockSlim>。  <xref:System.Threading.ReaderWriterLockSlim> 类似于 <xref:System.Threading.ReaderWriterLock>，但简化了递归规则以及升级和降级锁定状态的规则。  <xref:System.Threading.ReaderWriterLockSlim> 可避免多种潜在的死锁情况。  此外，<xref:System.Threading.ReaderWriterLockSlim> 的性能明显优于 <xref:System.Threading.ReaderWriterLock>。  
  
## 请参阅  
 <xref:System.Threading.ReaderWriterLockSlim>   
 <xref:System.Threading.ReaderWriterLock>   
 [Threading](../../../docs/standard/threading/index.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)