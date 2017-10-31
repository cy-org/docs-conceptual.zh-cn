---
title: "Using Threads and Threading | Microsoft Docs"
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
  - "threading [.NET Framework], about threading"
  - "managed threading"
ms.assetid: 9b5ec2cd-121b-4d49-b075-222cf26f2344
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Using Threads and Threading
本节中的主题讨论托管线程的创建和管理，如何将数据传递到托管线程和返回结果，以及如何销毁线程和处理 <xref:System.Threading.ThreadAbortException>。  
  
## 本节内容  
 [Creating Threads and Passing Data at Start Time](../../../docs/standard/threading/creating-threads-and-passing-data-at-start-time.md)  
 讨论并演示如何创建托管线程，包括如何将数据传递到新线程以及如何返回数据。  
  
 [Pausing and Resuming Threads](../../../docs/standard/threading/pausing-and-resuming-threads.md)  
 讨论暂停和继续执行托管线程的后果。  
  
 [Destroying Threads](../../../docs/standard/threading/destroying-threads.md)  
 讨论销毁托管线程的后果，以及如何处理 <xref:System.Threading.ThreadAbortException>。  
  
 [Scheduling Threads](../../../docs/standard/threading/scheduling-threads.md)  
 讨论线程优先级及它们如何影响线程调度。  
  
## 参考  
 <xref:System.Threading.Thread>  
 提供 <xref:System.Threading.Thread> 类的参考文档，该类表示托管线程（无论它是来自非托管代码还是在托管应用程序中创建的）。  
  
 <xref:System.Threading.ThreadStart>  
 提供表示无参数线程过程的 <xref:System.Threading.ThreadStart> 委托的参考文档。  
  
 <xref:System.Threading.ParameterizedThreadStart>  
 提供一种在不使用强类型时也能将数据传递到线程过程的简便方式。  
  
## 相关章节  
 [Threads and Threading](../../../docs/standard/threading/threads-and-threading.md)  
 提供对托管线程处理的介绍。