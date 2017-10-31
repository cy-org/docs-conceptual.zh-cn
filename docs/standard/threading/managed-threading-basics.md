---
title: "Managed Threading Basics | Microsoft Docs"
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
  - "multiple threads"
  - "threading [.NET Framework], multiple threads"
  - "threading [.NET Framework], about threading"
  - "managed threading"
ms.assetid: b2944911-0e8f-427d-a8bb-077550618935
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Managed Threading Basics
本节的前五个主题旨在帮助您确定何时使用托管线程处理，并解释了一些基本功能。  有关提供其他功能的类的信息，请参见 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md) 和 [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md)。  
  
 本节其余的主题讨论的是一些高级主题，包括托管线程处理与 Windows 操作系统的交互。  
  
> [!NOTE]
>  在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]中，任务并行库和 PLINQ 为多线程程序中的任务和数据并行提供了 API。  有关更多信息，请参见 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)。  
  
## 本节内容  
 [Threads and Threading](../../../docs/standard/threading/threads-and-threading.md)  
 讨论多线程的优缺点，并概括了可以创建线程或使用线程池线程的几种情形。  
  
 [Exceptions in Managed Threads](../../../docs/standard/threading/exceptions-in-managed-threads.md)  
 描述不同版本 .NET Framework 的线程中的未经处理的异常的行为，尤其是导致应用程序终止时的行为。  
  
 [Synchronizing Data for Multithreading](../../../docs/standard/threading/synchronizing-data-for-multithreading.md)  
 描述将用于多线程的同步类中的数据的策略。  
  
 [托管线程状态](../../../docs/standard/threading/managed-thread-states.md)  
 描述基本的线程状态，并解释如何检测一个线程是否在运行。  
  
 [Foreground and Background Threads](../../../docs/standard/threading/foreground-and-background-threads.md)  
 解释了前台和后台线程的区别。  
  
 [Managed and Unmanaged Threading in Windows](../../../docs/standard/threading/managed-and-unmanaged-threading-in-windows.md)  
 讨论了托管和非托管线程处理之间的关系，列出了 Windows 线程处理 API 的托管等效项，并讨论了 COM 单元和托管线程之间的交互。  
  
 [Thread.Suspend, Garbage Collection, and Safe Points](../../../docs/standard/threading/thread-suspend-garbage-collection-and-safe-points.md)  
 描述线程挂起和垃圾回收。  
  
 [Thread Local Storage: Thread\-Relative Static Fields and Data Slots](../../../docs/standard/threading/thread-local-storage-thread-relative-static-fields-and-data-slots.md)  
 描述线程相关的存储机制。  
  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)  
 描述可如何通过使用取消标记取消异步或长期运行的同步操作。  
  
## 参考  
 <xref:System.Threading.Thread>  
 提供 **Thread** 类的参考文档，该类表示托管线程（无论它是来自非托管代码还是在托管应用程序中创建的）。  
  
 <xref:System.ComponentModel.BackgroundWorker>  
 为结合用户界面对象与多线程处理提供了一种安全方法。  
  
## 相关章节  
 [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md)  
 介绍用于同步多个线程的活动的托管类。  
  
 [Managed Threading Best Practices](../../../docs/standard/threading/managed-threading-best-practices.md)  
 介绍多线程处理的常见问题以及避免这些问题的策略。  
  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)  
 描述任务并行库和 PLINQ，它们极大简化了创建异步和多线程 .NET Framework 应用程序的工作。