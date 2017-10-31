---
title: "托管线程处理"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- threading [.NET Framework], about threading
- managed threading
ms.assetid: 7b46a7d9-c6f1-46d1-a947-ae97471bba87
caps.latest.revision: 19
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: f2a8792818e837f019403aa84c2c2e98db0b2b89
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="managed-threading"></a>托管线程处理
无论是要为具有一个还是多个处理器的计算机进行开发，你都希望应用程序能够提供响应最为迅速的用户交互，即使应用程序当前正在执行其他操作，也不例外。 使用多线程执行是让应用程序一直迅速响应用户的最有效方式，同时也是在用户事件之间或在用户事件期间使用处理器的最有效方式。 虽然本部分介绍的是线程基本概念，但将会重点介绍托管线程概念和如何使用托管线程。  
  
> [!NOTE]
>  自 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 起，由于出现了 <xref:System.Threading.Tasks.Parallel?displayProperty=fullName> 和 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 类、[并行 LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)、<xref:System.Collections.Concurrent?displayProperty=fullName> 命名空间中的新并发集合类以及基于任务（而非线程）概念的新编程模型，多线程编程大大得到了简化。 有关详细信息，请参阅[并行编程](../../../docs/standard/parallel-programming/index.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [托管线程处理基本知识](../../../docs/standard/threading/managed-threading-basics.md)  
 概述了托管线程以及何时使用多线程。  
  
 [使用线程和线程处理](../../../docs/standard/threading/using-threads-and-threading.md)  
 介绍了如何创建、启动、暂停、恢复和中止线程。  
  
 [托管线程处理的最佳做法](../../../docs/standard/threading/managed-threading-best-practices.md)  
 介绍了同步级别、如何避免死锁和争用条件、单处理器和多处理器计算机以及其他线程问题。  
  
 [线程处理对象和功能](../../../docs/standard/threading/threading-objects-and-features.md)  
 介绍了可用于同步在不同线程上访问的线程活动和对象数据的托管类，并概述了线程池线程。  
  
## <a name="reference"></a>参考  
 <xref:System.Threading>  
 收录了用于使用和同步托管线程的类。  
  
 <xref:System.Collections.Concurrent>  
 收录了可安全用于多线程的集合类。  
  
 <xref:System.Threading.Tasks>  
 收录了用于创建和计划并发处理任务的类。  
  
## <a name="related-sections"></a>相关章节  
 [应用程序域](../../../docs/framework/app-domains/application-domains.md)  
 概述了应用程序域及其在公共语言基础结构中的应用。  
  
 [异步文件 I/O](../../../docs/standard/io/asynchronous-file-i-o.md)  
 描述异步 I/O 的性能优势和基本操作。  
  
 [基于事件的异步模式 (EAP)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)  
 概述了异步编程。  
  
 [使用异步方式调用同步方法](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)  
 介绍了如何使用委托的内置功能对线程池线程调用方法。  
  
 [并行编程](../../../docs/standard/parallel-programming/index.md)  
 介绍了并行编程库，其简化了在应用程序中使用多线程。  
  
 [并行 LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)  
 介绍了为利用多个处理器而并行运行查询的系统。

