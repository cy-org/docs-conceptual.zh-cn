---
title: "Synchronizing Data for Multithreading | Microsoft Docs"
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
  - "synchronization, threads"
  - "threading [.NET Framework], synchronizing threads"
  - "managed threading"
ms.assetid: b980eb4c-71d5-4860-864a-6dfe3692430a
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Synchronizing Data for Multithreading
当多个线程可以调用单个对象的属性和方法时，对这些调用进行同步处理是非常重要的。  否则，一个线程可能会中断另一个线程正在执行的任务，使该对象处于一种无效状态。  其成员不受这类中断影响的类叫做线程安全类。  
  
 Common Language Infrastructure 提供了几种可用来同步对实例和静态成员的访问的策略：  
  
-   同步代码区域。  可以使用 <xref:System.Threading.Monitor> 类或此类的编译器支持来仅同步需要此类的代码块，从而提高性能。  
  
-   手动同步。  可以使用 .NET Framework 类库提供的同步对象。  请参见 [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md)，这部分对 <xref:System.Threading.Monitor> 类进行了讨论。  
  
-   同步上下文。  可以使用 <xref:System.Runtime.Remoting.Contexts.SynchronizationAttribute> 为 <xref:System.ContextBoundObject> 对象启用简单的自动同步。  
  
-   <xref:System.Collections.Concurrent?displayProperty=fullName> 命名空间中的集合类。  这些类提供了内置的同步添加和移除操作。  有关更多信息，请参见[线程安全集合](../../../docs/standard/collections/thread-safe/index.md)。  
  
 公共语言运行时提供一个线程模型，在该模型中，类分为许多类别，这些类别可以根据要求以各种不同的方式进行同步。  下表显示了为具有给定同步类别的字段和方法提供的同步支持。  
  
|类别|全局字段|静态字段|静态方法|实例字段|实例方法|特定代码块|  
|--------|----------|----------|----------|----------|----------|-----------|  
|无同步|否|否|否|否|否|否|  
|同步上下文|否|否|否|是|是|否|  
|同步代码区域|否|否|仅当标记时|否|仅当标记时|仅当标记时|  
|手动同步|手动|手动|手动|手动|手动|手动|  
  
## 无同步  
 这对于对象是默认情况。  任何线程都可以随时访问任何方法或字段。  一次只能有一个线程访问这些对象。  
  
## 手动同步  
 .NET Framework 类库提供大量用于同步线程的类。  请参见 [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md)。  
  
## 同步代码区域  
 可以使用 <xref:System.Threading.Monitor> 类或编译器关键字来同步代码块、实例方法和静态方法。  不支持同步静态字段。  
  
 Visual Basic 和 C\# 都支持使用特定语言关键字标记代码块，在 C\# 中使用的是 `lock` 语句，在 Visual Basic 中使用的是 `SyncLock` 语句。  当由线程执行该代码时，会尝试获取锁。  如果该锁已由其他线程获取，则在锁变为可用状态之前，该线程一直处于禁止状态。  当线程退出同步代码块时，锁就会被释放，它与线程的退出方式无关。  
  
> [!NOTE]
>  `lock` 和 `SyncLock` 语句是使用 <xref:System.Threading.Monitor.Enter%2A?displayProperty=fullName> 和 <xref:System.Threading.Monitor.Exit%2A?displayProperty=fullName> 实现的，因此，可以在同步区域中将它们与 <xref:System.Threading.Monitor> 的其他方法一起使用。  
  
 还可以用 **MethodImplAttribute** 和 **MethodImplOptions.Synchronized** 修饰方法，其效果和使用 **Monitor** 或其中一个编译器关键字锁定整个方法体相同。  
  
 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> 可用于使线程跳出阻止操作（如等待访问同步代码区域）。  **Thread.Interrupt** 还用于使线程跳出 <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName> 等操作。  
  
> [!IMPORTANT]
>  为保护 `static` 方法（Visual Basic 中的 `Shared` 方法），请不要锁定类型，即：C\# 中的 `typeof(MyType)`、Visual Basic 中的 `GetType(MyType)` 或 C\+\+ 中的 `MyType::typeid`。  而应改用私有静态对象。  类似地，不要使用 C\# 中的 `this`（Visual Basic 中的 `Me`）锁定实例方法。  而应使用私有对象。  类或实例可由其他代码锁定，您自己的代码进行锁定可能会引起死锁或性能问题。  
  
### 编译器支持  
 Visual Basic 和 C\# 都支持使用 <xref:System.Threading.Monitor.Enter%2A?displayProperty=fullName> 和 <xref:System.Threading.Monitor.Exit%2A?displayProperty=fullName> 来锁定对象的语言关键字。  Visual Basic 支持 [SyncLock](../../../ocs/visual-basic/language-reference/statements/synclock-statement.md) 语句；C\# 支持 [lock](../Topic/lock%20Statement%20\(C%23%20Reference\).md) 语句。  
  
 这两种情况下，如果代码块中引发异常，则 **lock** 或 **SyncLock** 锁获取的锁将自动释放。  C\# 和 Visual Basic 编译器在发出 **try**\/**finally** 块时，在 try 的起始处使用 **Monitor.Enter**，在 **finally** 块中使用 **Monitor.Exit**。  如果 **lock** 或 **SyncLock** 块内部引发了异常，则会运行 **finally** 处理程序，从而使您可以执行任何清除工作。  
  
## 同步上下文  
 可以使用任何 **ContextBoundObject** 的 **SynchronizationAttribute** 来同步所有实例方法和字段。  同一上下文域中的所有对象都共享同一个锁。  允许多个线程访问方法和字段，但在任一时刻只允许一个线程访问。  
  
## 请参阅  
 <xref:System.Runtime.Remoting.Contexts.SynchronizationAttribute>   
 [Threads and Threading](../../../docs/standard/threading/threads-and-threading.md)   
 [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md)   
 [SyncLock 语句](../../../ocs/visual-basic/language-reference/statements/synclock-statement.md)   
 [“锁定”语句](../Topic/lock%20Statement%20\(C%23%20Reference\).md)