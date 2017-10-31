---
title: "How to: Enable Thread-Tracking Mode in SpinLock | Microsoft Docs"
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
  - "SpinLock, how to enable thread-tracking"
ms.assetid: 62ee2e68-0bdd-4869-afc9-f0a57a11ae01
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Enable Thread-Tracking Mode in SpinLock
<xref:System.Threading.SpinLock?displayProperty=fullName> 是一个低级别的互斥锁，可用于等待时间非常短的场合。  <xref:System.Threading.SpinLock> 不是可重入的。  在线程进入锁之后，它必须先正确地退出锁，然后才能再次进入锁。  通常，任何重新进入锁的尝试都会导致死锁，并且死锁非常难调试。  作为开发的辅助手段，<xref:System.Threading.SpinLock?displayProperty=fullName> 支持一种线程跟踪模式，当线程尝试重新进入它已经持有的锁时，此模式将会导致引发异常。  这将让您更易于定位到锁未正确退出的点。  通过使用一个采用布尔输入形参的 <xref:System.Threading.SpinLock> 构造函数并传入 `true` 实参，可以启用线程跟踪模式。  完成开发和测试阶段之后，应关闭线程跟踪模式以获得更好的性能。  
  
## 示例  
 下面的代码示例阐释了线程跟踪模式。  示例中的用于正确退出锁的代码行都被注释掉了，以便模拟导致以下结果之一的编码错误：  
  
-   如果通过使用 `true`（在 Visual Basic 中为 `True`）参数来创建 <xref:System.Threading.SpinLock>，则引发异常。  
  
-   如果通过使用 `false`（在 Visual Basic 中为 `False`）参数来创建 <xref:System.Threading.SpinLock>，则导致死锁。  
  
 [!code-csharp[CDS_SpinLock#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinlock/cs/spinlockdemo.cs#01)]
 [!code-vb[CDS_SpinLock#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinlock/vb/spinlock_threadtracking.vb#01)]  
  
## 请参阅  
 [SpinLock](../../../docs/standard/threading/spinlock.md)