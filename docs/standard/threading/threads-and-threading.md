---
title: "Threads and Threading | Microsoft Docs"
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
  - "threading [.NET Framework]"
  - "threading [.NET Framework], multiple threads"
ms.assetid: 5baac3aa-e603-4fa6-9f89-0f2c1084e6b1
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Threads and Threading
操作系统使用进程将它们正在执行的不同应用程序分开。  线程是操作系统分配处理器时间的基本单元，并且进程中可以有多个线程同时执行代码。  每个线程都维护异常处理程序、调度优先级和一组系统用于在调度该线程前保存线程上下文的结构。  线程上下文包括为使线程在线程的宿主进程地址空间中无缝地继续执行所需的所有信息，包括线程的 CPU 寄存器组和堆栈。  
  
 .NET Framework 将操作系统进程进一步细分为由 <xref:System.AppDomain?displayProperty=fullName> 表示的、称为应用程序域的轻量托管子进程。  一个或多个托管线程（由 <xref:System.Threading.Thread?displayProperty=fullName> 表示）可以在同一个托管进程中的一个或任意数目的应用程序域中运行。  虽然每个应用程序域都是用单个线程启动的，但该应用程序域中的代码可以创建附加应用程序域和附加线程。  其结果是托管线程可以在同一个非托管进程中的应用程序域之间自由移动；您可能只有一个线程在若干应用程序域之间移动。  
  
 支持抢先多任务处理的操作系统可以创建多个进程中的多个线程同时执行的效果。  它通过以下方式实现这一点：在需要处理器时间的线程之间分割可用处理器时间，并轮流为每个线程分配处理器时间片。  当前执行的线程在其时间片结束时被挂起，而另一个线程继续运行。  当系统从一个线程切换到另一个线程时，它将保存被抢先的线程的线程上下文，并重新加载线程队列中下一个线程的已保存线程上下文。  
  
 时间片的长度取决于操作系统和处理器。  由于每个时间片都很小，因此即使只有一个处理器，多个线程看起来似乎也是在同时执行。  这实际上就是多处理器系统中发生的情形，在此类系统中，可执行线程分布在多个可用处理器中。  
  
## 何时使用多个线程  
 需要用户交互的软件必须尽可能快地对用户的活动作出反应，以便提供丰富多彩的用户体验。  但同时它必须执行必要的计算以便尽可能快地将数据呈现给用户。  如果应用程序仅使用一个执行线程，则可以将[异步编程](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)与 [.NET Framework 远程处理](http://msdn.microsoft.com/zh-cn/eccb1d31-0a22-417a-97fd-f4f1f3aa4462)或使用 ASP.NET 创建的 [XML Web services](http://msdn.microsoft.com/zh-cn/1e64af78-d705-4384-b08d-591a45f4379c) 结合使用，在使用自己的计算机的处理时间之外还使用其他计算机的处理时间，从而提高对用户的响应速度并减少应用程序的数据处理时间。  如果您正在进行大量的输入\/输出工作，则还可以使用 I\/O 完成端口来提高应用程序的响应速度。  
  
### 多个线程的优点  
 无论如何，要提高对用户的响应速度并且处理所需数据以便几乎同时完成工作，使用多个线程是一种最为强大的技术。  在具有一个处理器的计算机上，多个线程可以通过利用用户事件之间很小的时间段在后台处理数据来达到这种效果。  例如，在另一个线程正在重新计算同一应用程序中的电子表格的其他部分时，用户可以编辑该电子表格。  
  
 无需修改，同一个应用程序在具有多个处理器的计算机上运行时将极大地满足用户的需要。  单个应用程序域可以使用多个线程来完成以下任务：  
  
-   通过网络与 Web 服务器和数据库进行通信。  
  
-   执行占用大量时间的操作。  
  
-   区分具有不同优先级的任务。  例如，高优先级线程管理时间关键的任务，低优先级线程执行其他任务。  
  
-   使用户界面可以在将时间分配给后台任务时仍能快速做出响应。  
  
### 多个线程的缺点  
 建议您使用尽可能少的线程，这样可以最大限度地减少操作系统资源的使用，并可提高性能。  线程处理还具有在设计应用程序时要考虑的资源要求和潜在冲突。  这些资源要求如下所述：  
  
-   系统将为进程、**AppDomain** 对象和线程所需的上下文信息使用内存。  因此，可以创建的进程、**AppDomain** 对象和线程的数目会受到可用内存的限制。  
  
-   跟踪大量的线程将占用大量的处理器时间。  如果线程过多，则其中大多数线程都不会产生明显的进度。  如果大多数当前线程处于一个进程中，则其他进程中的线程的调度频率就会很低。  
  
-   使用许多线程控制代码执行非常复杂，并可能产生许多 bug。  
  
-   销毁线程需要了解可能发生的问题并对那些问题进行处理。  
  
 提供对资源的共享访问会造成冲突。  为了避免冲突，必须对共享资源进行同步或控制对共享资源的访问。  如果在相同或不同的应用程序域中未能正确地使访问同步，则会导致出现一些问题，这些问题包括死锁和争用条件等，其中死锁是指两个线程都停止响应，并且都在等待对方完成；争用条件是指由于意外地出现对两个事件的执行时间的临界依赖性而发生反常的结果。  系统提供了可用于协调多个线程之间的资源共享的同步对象。  减少线程的数目使同步资源更为容易。  
  
 需要同步的资源包括：  
  
-   系统资源（如通信端口）。  
  
-   多个进程所共享的资源（如文件句柄）。  
  
-   由多个线程访问的单个应用程序域的资源（如全局、静态和实例字段）。  
  
### 线程处理与应用程序设计  
 一般情况下，要为不会阻止其他线程的相对较短的任务处理多个线程并且不需要对这些任务执行任何特定调度时，使用 <xref:System.Threading.ThreadPool> 类是一种最简单的方式。  但是，有多个理由创建您自己的线程：  
  
-   如果您需要使一个任务具有特定的优先级。  
  
-   如果您具有可能会长时间运行（并因此阻止其他任务）的任务。  
  
-   如果您需要将线程放置到单线程单元中（所有 **ThreadPool** 线程均处于多线程单元中）。  
  
-   如果您需要与该线程关联的稳定标识。  例如，您应使用一个专用线程来中止该线程，将其挂起或按名称发现它。  
  
-   如果您需要运行与用户界面交互的后台线程，.NET Framework 2.0 版提供了 <xref:System.ComponentModel.BackgroundWorker> 组件，该组件可以使用事件与用户界面线程的跨线程封送进行通信。  
  
### 线程处理和异常  
 在线程中执行异常处理。  线程（甚至是后台线程）中的未经处理的异常通常会终止进程。  以下为此规则的三种例外情况：  
  
-   由于调用了 <xref:System.Threading.Thread.Abort%2A>，线程中将引发 <xref:System.Threading.ThreadAbortException>。  
  
-   由于正在卸载应用程序域，线程中将引发 <xref:System.AppDomainUnloadedException>。  
  
-   公共语言运行时或宿主进程将终止线程。  
  
 有关更多信息，请参见[Exceptions in Managed Threads](../../../docs/standard/threading/exceptions-in-managed-threads.md)。  
  
> [!NOTE]
>  在 .NET Framework 1.0 和 1.1 版中，公共语言运行时将捕获一些异常（例如在线程池线程中），而不出现任何提示。  这可能会破坏应用程序状态，并最终导致应用程序挂起，将很难进行调试。  
  
## 请参阅  
 <xref:System.Threading.ThreadPool>   
 <xref:System.ComponentModel.BackgroundWorker>   
 [Synchronizing Data for Multithreading](../../../docs/standard/threading/synchronizing-data-for-multithreading.md)   
 [The Managed Thread Pool](../../../docs/standard/threading/the-managed-thread-pool.md)