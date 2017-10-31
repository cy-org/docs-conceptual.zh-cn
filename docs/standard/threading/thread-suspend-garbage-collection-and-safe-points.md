---
title: "Thread.Suspend, Garbage Collection, and Safe Points | Microsoft Docs"
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
  - "suspending threads"
  - "safe points"
  - "threading [.NET Framework], suspending"
  - "threading [.NET Framework], garbage collection"
  - "garbage collection, threads"
ms.assetid: e8f58e17-2714-4821-802a-f8eb3b2baa62
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Thread.Suspend, Garbage Collection, and Safe Points
对某线程调用 <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> 时，系统会注意到已经请求了线程挂起，并且会让该线程执行到一个安全点，然后才实际挂起该线程。  线程的安全点是线程执行过程中可执行垃圾回收的一个点。  
  
 到达安全点时，运行时就会确保挂起的线程将不在托管代码中再执行任何进一步的操作。  在托管代码之外执行的线程总可以安全地进行垃圾回收，而且在它尝试恢复托管代码的执行时将继续执行托管代码。  
  
> [!NOTE]
>  为了执行垃圾回收，运行时必须挂起除正在执行回收的线程以外的所有线程。  每个线程在可以挂起之前都必须置于安全点。  
  
## 请参阅  
 <xref:System.Threading.Thread>   
 <xref:System.GC>   
 [Threading](../../../docs/standard/threading/index.md)   
 [自动内存管理](../../../docs/standard/automatic-memory-management.md)