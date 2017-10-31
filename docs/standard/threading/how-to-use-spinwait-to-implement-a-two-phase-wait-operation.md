---
title: "How to: Use SpinWait to Implement a Two-Phase Wait Operation | Microsoft Docs"
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
  - "SpinWait, how to synchronize two-phase wait"
ms.assetid: b2ac4e4a-051a-4f65-b4b9-f8e103aff195
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Use SpinWait to Implement a Two-Phase Wait Operation
下面的示例演示如何使用 <xref:System.Threading.SpinWait?displayProperty=fullName> 对象实现两阶段等待操作。  在第一个阶段中，同步对象 `Latch` 会旋转几个周期，并同时检查锁是否变为可用。  在第二个阶段中，如果锁变为可用，则 `Wait` 方法将返回而不必使用 <xref:System.Threading.ManualResetEvent?displayProperty=fullName> 来执行其等待；否则 `Wait` 将执行等待。  
  
## 示例  
 本示例演示了闩锁同步基元的一个非常基本的实现。  当等待时间预计非常短时，可以使用此数据结构。  此示例仅供演示使用。  如果在程序中需要闩锁类型功能，请考虑使用 <xref:System.Threading.ManualResetEventSlim?displayProperty=fullName>。  
  
 [!code-csharp[CDS_SpinWait#03](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinwait/cs/spinwait03.cs#03)]
 [!code-vb[CDS_SpinWait#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinwait/vb/spinwait2.vb#03)]  
  
 闩锁使用 <xref:System.Threading.SpinWait> 对象就地旋转，直至下一个对 `SpinOnce` 的调用导致 <xref:System.Threading.SpinWait> 让出线程的时间片。  此时，通过对 <xref:System.Threading.ManualResetEvent> 调用 <xref:System.Threading.WaitHandle.WaitOne%2A> 并递入超时值的剩余部分，闩锁会导致其自身的上下文切换。  
  
 日志输出显示了闩锁能够在不使用 <xref:System.Threading.ManualResetEvent> 的情况下通过获取锁来提高性能的频率。  
  
## 请参阅  
 [SpinWait](../../../docs/standard/threading/spinwait.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)