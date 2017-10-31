---
title: "Scheduling Threads | Microsoft Docs"
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
  - "threading [.NET Framework], scheduling"
  - "scheduling threads"
ms.assetid: 67e4a0eb-3095-4ea7-b20f-908faa476277
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Scheduling Threads
每个线程都具有分配给它的线程优先级。  为在公共语言运行时中创建的线程最初分配的优先级为 **ThreadPriority.Normal**。  在运行时外创建的线程会保留它们在进入托管环境之前所具有的优先级。  您可以使用 **Thread.Priority** 属性获取或设置任何线程的优先级。  
  
 线程是根据其优先级而调度执行的。  即使线程正在运行时中执行，所有线程都是由操作系统分配处理器时间片的。  用于确定线程执行顺序的调度算法的详细情况随每个操作系统的不同而不同。  在某些操作系统下，具有最高优先级（相对于可执行线程而言）的线程经过调度后总是首先运行。  如果具有相同优先级的多个线程都可用，则计划程序将遍历处于该优先级的线程，并为每个线程提供一个固定的时间片来执行。  只要具有较高优先级的线程可以运行，具有较低优先级的线程就不会执行。  如果在给定的优先级上不再有可运行的线程，则计划程序将移到下一个较低的优先级并在该优先级上调度线程以执行。  如果具有较高优先级的线程可以运行，则具有较低优先级的线程将被抢先，并允许具有较高优先级的线程再次执行。  除此之外，当应用程序的用户界面在前台和后台之间移动时，操作系统还可以动态调整线程优先级。  其他操作系统可以选择使用不同的调度算法。  
  
## 请参阅  
 [Using Threads and Threading](../../../docs/standard/threading/using-threads-and-threading.md)   
 [Managed and Unmanaged Threading in Windows](../../../docs/standard/threading/managed-and-unmanaged-threading-in-windows.md)